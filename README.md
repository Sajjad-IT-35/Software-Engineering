# Software-Engineering
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: ConversionPage(),
    );
  }
}

class ConversionPage extends StatefulWidget {
  @override
  _ConversionPageState createState() => _ConversionPageState();
}

class _ConversionPageState extends State<ConversionPage> {
  final TextEditingController _controller = TextEditingController();
  String _fromUnit = 'Miles';
  String _toUnit = 'Kilometers';
  double _result = 0;

  // Conversion logic
  void _convert() {
    double value = double.tryParse(_controller.text) ?? 0;

    if (_fromUnit == 'Miles' && _toUnit == 'Kilometers') {
      _result = value * 1.60934;
    } else if (_fromUnit == 'Kilometers' && _toUnit == 'Miles') {
      _result = value / 1.60934;
    } else if (_fromUnit == 'Kilograms' && _toUnit == 'Pounds') {
      _result = value * 2.20462;
    } else if (_fromUnit == 'Pounds' && _toUnit == 'Kilograms') {
      _result = value / 2.20462;
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Unit Converter'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: <Widget>[
            // Input Field
            TextField(
              controller: _controller,
              decoration: InputDecoration(
                labelText: 'Enter value to convert',
              ),
              keyboardType: TextInputType.number,
            ),
            SizedBox(height: 20),

            // From Unit Dropdown
            DropdownButton<String>(
              value: _fromUnit,
              onChanged: (String? newValue) {
                setState(() {
                  _fromUnit = newValue!;
                });
              },
              items: <String>['Miles', 'Kilometers', 'Kilograms', 'Pounds']
                  .map<DropdownMenuItem<String>>((String value) {
                return DropdownMenuItem<String>(
                  value: value,
                  child: Text(value),
                );
              }).toList(),
            ),
            SizedBox(height: 20),

            // To Unit Dropdown
            DropdownButton<String>(
              value: _toUnit,
              onChanged: (String? newValue) {
                setState(() {
                  _toUnit = newValue!;
                });
              },
              items: <String>['Miles', 'Kilometers', 'Kilograms', 'Pounds']
                  .map<DropdownMenuItem<String>>((String value) {
                return DropdownMenuItem<String>(
                  value: value,
                  child: Text(value),
                );
              }).toList(),
            ),
            SizedBox(height: 20),

            // Convert Button
            ElevatedButton(
              onPressed: () {
                setState(() {
                  _convert();
                });
              },
              child: Text('Convert'),
            ),
            SizedBox(height: 20),

            // Result Text
            Text(
              'Result: $_result',
              style: TextStyle(fontSize: 24),
            ),
          ],
        ),
      ),
    );
  }
}
