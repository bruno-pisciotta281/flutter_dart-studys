# PROVA
<br id="topo">

<div align="center">
  
 <p>Implemenar um aplicativo em flutter de acordo com as seguintes funcionalidades:
Tela de entrada de login: solicitar username e password 
Permitir acesso a segunda tela, somente se login for válido (login estático, permitir acesso somente se username="teste" e password="123", se não fornecer username, password ou  informações diferente do acesso permitido, informar "Acesso não permitido" ou "fornecer informações para acesso", conforme o caso.
A segunda tela deve mostrar uma lista (utilizando checkbox), onde o usuário deverá indicar quais tecnologias de desenvolvimento mobile, tem conhecimento. As opções sao: Flutter, React Native, Kotlin, Java, Ionic.
A segunda tela deve conter um boão "enviar", ao selecionar o botão, as opções selecionadas no checkbox devem ser enviadas por parâmetro para uma terceira tela e visualizá-las em um listview, com a mensagem de texto (após o listview) indicando "informações enviadas ao servidor" (simulação apenas).</p>

 ![](https://github.com/bruno-pisciotta281/flutter_dart-studys/blob/PROVA/Untitled%20video%20-%20Made%20with%20Clipchamp%20(1).gif)
  
</div>

<br>
- Códigos para rodar a aplicação (feita utilizando a plataforma (https://zapp.run)


```bash
  import 'package:flutter/material.dart';

  void main() {
    runApp(LoginApp());
  }

  class LoginApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        theme: ThemeData(
          appBarTheme: AppBarTheme(
            backgroundColor: Color(0xFF008080),
          ),
          elevatedButtonTheme: ElevatedButtonThemeData(
            style: ButtonStyle(
              backgroundColor: MaterialStateProperty.all<Color>(Color(0xFF008080)),
            ),
          ),
          textButtonTheme: TextButtonThemeData(
            style: ButtonStyle(
              foregroundColor: MaterialStateProperty.all<Color>(Colors.white),
            ),
          ),
          dialogTheme: DialogTheme(
            backgroundColor: Colors.white,
            titleTextStyle: TextStyle(
              color: Color(0xFF008080),
              fontWeight: FontWeight.bold,
            ),
            contentTextStyle: TextStyle(
              color: Color(0xFF008080),
            ),
          ),
        ),
        home: LoginPage(),
        routes: {
          '/selection': (context) => SelectionPage(),
        },
      );
    }
  }

  class LoginPage extends StatefulWidget {
    @override
    _LoginPageState createState() => _LoginPageState();
  }

  class _LoginPageState extends State<LoginPage> {
    TextEditingController _usernameController = TextEditingController();
    TextEditingController _passwordController = TextEditingController();
    String _message = '';

    void _login() {
      String username = _usernameController.text.trim();
      String password = _passwordController.text.trim();

      if (username == 'teste' && password == '123') {
        Navigator.pushNamed(context, '/selection');
      } else {
        showDialog(
          context: context,
          builder: (BuildContext context) {
            return AlertDialog(
              title: Text(
                'Acesso não permitido',
                style: Theme.of(context).dialogTheme.titleTextStyle,
              ),
              content: Text(
                'Nome de Usuário ou Senha errados',
                style: Theme.of(context).dialogTheme.contentTextStyle,
              ),
              actions: <Widget>[
                TextButton(
                  onPressed: () {
                    Navigator.of(context).pop();
                  },
                  child: Text(
                    'OK',
                    style: TextStyle(
                      color: Color(0xFF008080),
                    ),
                  ),
                ),
              ],
            );
          },
        );
      }
    }

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Bem Vindo, faça Login para acessar!'),
        ),
        body: Container(
          padding: EdgeInsets.all(20.0),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              TextField(
                controller: _usernameController,
                decoration: InputDecoration(
                  hintText: 'Nome de Usuário',
                ),
              ),
              SizedBox(height: 20.0),
              TextField(
                controller: _passwordController,
                decoration: InputDecoration(
                  hintText: 'Senha',
                ),
                obscureText: true,
              ),
              SizedBox(height: 20.0),
              ElevatedButton(
                onPressed: _login,
                child: Text('Logar'),
              ),
              SizedBox(height: 20.0),
              Text(
                _message,
                style: TextStyle(
                  color: Colors.red,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ],
          ),
        ),
      );
    }
  }

  class SelectionPage extends StatefulWidget {
    @override
    _SelectionPageState createState() => _SelectionPageState();
  }

  class _SelectionPageState extends State<SelectionPage> {
    List<String> selectedTechnologies = [];

    void _toggleTechnology(String technology) {
      setState(() {
        if (selectedTechnologies.contains(technology)) {
          selectedTechnologies.remove(technology);
        } else {
          selectedTechnologies.add(technology);
        }
      });
    }

    void _submitSelection() {
      if (selectedTechnologies.isEmpty) {
        showDialog(
          context: context,
          builder: (BuildContext context) {
            return AlertDialog(
              title: Text(
                'Atenção',
                style: Theme.of(context).dialogTheme.titleTextStyle,
              ),
              content: Text(
                'Selecione pelo menos uma tecnologia',
                style: Theme.of(context).dialogTheme.contentTextStyle,
              ),
              actions: <Widget>[
                TextButton(
                  onPressed: () {
                    Navigator.of(context).pop();
                  },
                  child: Text(
                    'OK',
                    style: TextStyle(
                      color: Colors.white,
                    ),
                  ),
                ),
              ],
            );
          },
        );
      } else {
        Navigator.push(
          context,
          MaterialPageRoute(
            builder: (context) => ResultPage(selectedTechnologies: selectedTechnologies),
          ),
        );
      }
    }

    @override
    Widget build(BuildContext context) {
      return Scaffold(
        appBar: AppBar(
          title: Text('Questionário de Tecnologias'),
        ),
        body: Container(
          padding: EdgeInsets.all(20.0),
          child: Column(
            children: <Widget>[
              Text(
                'Qual dessas tecnologias mobile você tem mais conhecimento?',
                style: TextStyle(
                  fontWeight: FontWeight.bold,
                  fontSize: 18.0,
                ),
              ),
              CheckboxListTile(
                title: Text('Flutter'),
                value: selectedTechnologies.contains('Flutter'),
                onChanged: (value) => _toggleTechnology('Flutter'),
              ),
              CheckboxListTile(
                title: Text('React Native'),
                value: selectedTechnologies.contains('React Native'),
                onChanged: (value) => _toggleTechnology('React Native'),
              ),
              CheckboxListTile(
                title: Text('Kotlin'),
                value: selectedTechnologies.contains('Kotlin'),
                onChanged: (value) => _toggleTechnology('Kotlin'),
              ),
              CheckboxListTile(
                title: Text('Java'),
                value: selectedTechnologies.contains('Java'),
                onChanged: (value) => _toggleTechnology('Java'),
              ),
              CheckboxListTile(
                title: Text('Ionic'),
                value: selectedTechnologies.contains('Ionic'),
                onChanged: (value) => _toggleTechnology('Ionic'),
              ),
              SizedBox(height: 20.0),
              ElevatedButton(
                onPressed: _submitSelection,
                child: Text('Enviar'),
              ),
            ],
          ),
        ),
      );
    }
  }

 class ResultPage extends StatelessWidget {
  final List<String> selectedTechnologies;

  ResultPage({required this.selectedTechnologies});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Finalização'),
      ),
      body: Container(
        padding: EdgeInsets.all(20.0),
        child: Column(
          children: <Widget>[
            Text(
              'Tecnologias selecionadas:',
              style: TextStyle(
                fontWeight: FontWeight.bold,
                fontSize: 18.0,
              ),
            ),
            SizedBox(height: 10.0),
            if (selectedTechnologies.isNotEmpty)
              Center(
                child: ListView.builder(
                  shrinkWrap: true,
                  itemCount: selectedTechnologies.length,
                  itemBuilder: (context, index) {
                    return ListTile(
                      title: Text(selectedTechnologies[index]),
                    );
                  },
                ),
              ),
            if (selectedTechnologies.isEmpty)
              Text(
                'Nenhuma tecnologia selecionada',
                style: TextStyle(
                  fontStyle: FontStyle.italic,
                ),
              ),
            SizedBox(height: 20.0),
            Text(
              'Informações enviadas ao servidor',
              style: TextStyle(
                fontWeight: FontWeight.bold,
              ),
            ),
          ],
        ),
      ),
    );
  }
}

```
<p align="right"><a href="#topo">Voltar ao Topo</p> 
