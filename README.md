# Navegação entre páginas

<br id="topo">

<div align="center">

<img src = 'https://github.com/bruno-pisciotta281/flutter_dart-studys/blob/Exercício-01/Formulário.jpeg'  width="500">

</div>

<br>
- Códigos para rodar a aplicação (feita utilizando a plataforma (https://zapp.run)


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
              final userData = UserData(
                nome: nomeController.text,
                endereco: enderecoController.text,
                numero: numeroController.text,
                complemento: complementoController.text,
                uf: ufController.text,
                cep: cepController.text,
              );

              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => UserDataPage(userData: userData),
                ),
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
    return ![
      nomeController.text,
      enderecoController.text,
      numeroController.text,
      complementoController.text,
      ufController.text,
      cepController.text,
    ].contains('');
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

class UserData {
  final String nome;
  final String endereco;
  final String numero;
  final String complemento;
  final String uf;
  final String cep;

  UserData({
    required this.nome,
    required this.endereco,
    required this.numero,
    required this.complemento,
    required this.uf,
    required this.cep,
  });
}

class UserDataPage extends StatelessWidget {
  final UserData userData;

  const UserDataPage({required this.userData});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Dados do Usuário'),
        backgroundColor: Color(0xFF008080),
      ),
      body: Padding(
        padding: EdgeInsets.all(16),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text('Nome: ${userData.nome}'),
            Text('Endereço: ${userData.endereco}'),
            Text('Número: ${userData.numero}'),
            Text('Complemento: ${userData.complemento}'),
            Text('UF: ${userData.uf}'),
            Text('CEP: ${userData.cep}'),
          ],
        ),
      ),
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Ex3 - Navegação entre páginas (Bruno Pisciotta)'),
        backgroundColor: Color(0xFF008080),
      ),
      body: Padding(
        padding: EdgeInsets.all(16),
        child: DataEntryWidget(),
      ),
    ),
  ));
}

```
<p align="right"><a href="#topo">Voltar ao Topo</p> 
