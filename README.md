# Widget para entrada de dados

- Códigos para rodar a aplicação (feita utilizando o site ([ZAPP](https://zapp.run)))

```bash
import 'package:flutter/material.dart';

class DataEntryWidget extends StatefulWidget {
  @override
  _DataEntryWidgetState createState() => _DataEntryWidgetState();
}

class _DataEntryWidgetState extends State<DataEntryWidget> {
  TextEditingController nomeController = TextEditingController();
  TextEditingController enderecoController = TextEditingController();
  TextEditingController numeroController = TextEditingController();
  TextEditingController complementoController = TextEditingController();
  TextEditingController ufController = TextEditingController();
  TextEditingController cepController = TextEditingController();

  bool isSubmitted = false;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        TextField(
          controller: nomeController,
          decoration: InputDecoration(
            labelText: 'Nome',
            errorText: isSubmitted && nomeController.text.isEmpty ? 'Campo obrigatório' : null,
          ),
        ),
        TextField(
          controller: enderecoController,
          decoration: InputDecoration(
            labelText: 'Endereço',
            errorText: isSubmitted && enderecoController.text.isEmpty ? 'Campo obrigatório' : null,
          ),
        ),
        TextField(
          controller: numeroController,
          decoration: InputDecoration(
            labelText: 'Número',
            errorText: isSubmitted && numeroController.text.isEmpty ? 'Campo obrigatório' : null,
          ),
        ),
        TextField(
          controller: complementoController,
          decoration: InputDecoration(
            labelText: 'Complemento',
            errorText: isSubmitted && complementoController.text.isEmpty ? 'Campo obrigatório' : null,
          ),
        ),
        TextField(
          controller: ufController,
          decoration: InputDecoration(
            labelText: 'UF',
            errorText: isSubmitted && ufController.text.isEmpty ? 'Campo obrigatório' : null,
          ),
        ),
        TextField(
          controller: cepController,
          decoration: InputDecoration(
            labelText: 'CEP',
            errorText: isSubmitted && cepController.text.isEmpty ? 'Campo obrigatório' : null,
          ),
        ),
        SizedBox(height: 16),
        ElevatedButton(
          onPressed: () {
            setState(() {
              isSubmitted = true;
            });

            if (_checkRequiredFields()) {
              showDialog(
                context: context,
                builder: (BuildContext context) {
                  return AlertDialog(
                    title: Text('Seus Dados Enviados:'),
                    content: Text(
                      'Nome: ${nomeController.text}\n'
                      'Endereço: ${enderecoController.text}\n'
                      'Número: ${numeroController.text}\n'
                      'Complemento: ${complementoController.text}\n'
                      'UF: ${ufController.text}\n'
                      'CEP: ${cepController.text}',
                    ),
                    actions: [
                      TextButton(
                        onPressed: () {
                          Navigator.of(context).pop();
                        },
                        child: Text('Fechar'),
                      ),
                    ],
                  );
                },
              );
            } else {
              showDialog(
                context: context,
                builder: (BuildContext context) {
                  return AlertDialog(
                    title: Text('Campos obrigatórios não preenchidos'),
                    content: Text('Por favor, preencha todos os campos obrigatórios.'),
                    actions: [
                      TextButton(
                        onPressed: () {
                          Navigator.of(context).pop();
                        },
                        child: Text('Fechar'),
                      ),
                    ],
                  );
                },
              );
            }
          },
          child: Text('Enviar'),
          style: ElevatedButton.styleFrom(
            primary: Color(0xFF008080),
          ),
        ),
      ],
    );
  }

  bool _checkRequiredFields() {
    bool isValid = true;

    if (nomeController.text.isEmpty ||
        enderecoController.text.isEmpty ||
        numeroController.text.isEmpty ||
        complementoController.text.isEmpty ||
        ufController.text.isEmpty ||
        cepController.text.isEmpty) {
      isValid = false;
    }

    return isValid;
  }

  @override
  void dispose() {
    nomeController.dispose();
    enderecoController.dispose();
    numeroController.dispose();
    complementoController.dispose();
    ufController.dispose();
    cepController.dispose();
    super.dispose();
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Ex.1 - Campos Formulário (Bruno Pisciotta)'),
        backgroundColor: Color(0xFF008080),
      ),
      body: Padding(
        padding: EdgeInsets.all(16),
        child: DataEntryWidget(),
      ),
    ),
  ));
}

