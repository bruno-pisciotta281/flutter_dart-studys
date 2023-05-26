# Uso de CheckBox e Respostas
<br id="topo">

<div align="center">

<img src = 'https://github.com/bruno-pisciotta281/flutter_dart-studys/blob/Exercício-04/Exercício%2004.jpeg'  width="500">
  
 ![](name-of-giphy.gif)

</div>

<br>
- Códigos para rodar a aplicação (feita utilizando a plataforma (https://zapp.run)


```bash
import 'package:flutter/material.dart';

class Question {
  final String question;
  final List<String> options;

  Question({required this.question, required this.options});
}

class QuestionPage extends StatefulWidget {
  @override
  _QuestionPageState createState() => _QuestionPageState();
}

class _QuestionPageState extends State<QuestionPage> {
  List<bool> selectedOptionsQuestion1 = [false, false, false];
  List<bool> selectedOptionsQuestion2 = [false, false, false];

  List<Question> questions = [
    Question(
      question: 'Pergunta 01: O que você acha sobre o Dart?',
      options: ['É fácil!', 'Meio Confuso...', 'Impossível!!!'],
    ),
    Question(
      question: 'Pergunta 02: Você tem gostado de Flutter?',
      options: ['Claro!', 'Mais ou menos...', 'Não!!!'],
    ),
  ];

  @override
  Widget build(BuildContext context) {
    bool noOptionsSelected1 = selectedOptionsQuestion1.every((option) => option == false);
    bool noOptionsSelected2 = selectedOptionsQuestion2.every((option) => option == false);

    return Scaffold(
      appBar: AppBar(
        title: Text('Ex04: Questionário sobre Dart e Flutter! (Bruno Pisciotta)'),
        backgroundColor: Color(0xFF008080),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              questions[0].question,
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 8),
            Column(
              children: List.generate(
                questions[0].options.length,
                (index) => CheckboxListTile(
                  value: selectedOptionsQuestion1[index],
                  onChanged: (value) {
                    setState(() {
                      selectedOptionsQuestion1[index] = value!;
                    });
                  },
                  title: Text(questions[0].options[index]),
                ),
              ),
            ),
            SizedBox(height: 16),
            Text(
              questions[1].question,
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 8),
            Column(
              children: List.generate(
                questions[1].options.length,
                (index) => CheckboxListTile(
                  value: selectedOptionsQuestion2[index],
                  onChanged: (value) {
                    setState(() {
                      selectedOptionsQuestion2[index] = value!;
                    });
                  },
                  title: Text(questions[1].options[index]),
                ),
              ),
            ),
            SizedBox(height: 16),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceEvenly,
              children: [
                ElevatedButton(
                  onPressed: () {
                    if (noOptionsSelected1) {
                      showDialog(
                        context: context,
                        builder: (BuildContext context) {
                          return AlertDialog(
                            title: Text('Nenhuma resposta foi selecionada'),
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
                            title: Text('Respostas - Pergunta 1'),
                            content: Column(
                              crossAxisAlignment: CrossAxisAlignment.start,
                              mainAxisSize: MainAxisSize.min,
                              children: [
                                if (selectedOptionsQuestion1[0])
                                  Text('- ${questions[0].options[0]}'),
                                if (selectedOptionsQuestion1[1])
                                  Text('- ${questions[0].options[1]}'),
                                if (selectedOptionsQuestion1[2])
                                  Text('- ${questions[0].options[2]}'),
                              ],
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
                    }
                  },
                  style: ButtonStyle(
                    backgroundColor: MaterialStateProperty.all<Color>(Color(0xFF008080)),
                  ),
                  child: Text('Visualizar Respostas - Pergunta 1'),
                ),
                ElevatedButton(
                  onPressed: () {
                    if (noOptionsSelected2) {
                      showDialog(
                        context: context,
                        builder: (BuildContext context) {
                          return AlertDialog(
                            title: Text('Nenhuma resposta foi selecionada'),
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
                            title: Text('Respostas - Pergunta 2'),
                            content: Column(
                              crossAxisAlignment: CrossAxisAlignment.start,
                              mainAxisSize: MainAxisSize.min,
                              children: [
                                if (selectedOptionsQuestion2[0])
                                  Text('- ${questions[1].options[0]}'),
                                if (selectedOptionsQuestion2[1])
                                  Text('- ${questions[1].options[1]}'),
                                if (selectedOptionsQuestion2[2])
                                  Text('- ${questions[1].options[2]}'),
                              ],
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
                    }
                  },
                  style: ButtonStyle(
                    backgroundColor: MaterialStateProperty.all<Color>(Color(0xFF008080)),
                  ),
                  child: Text('Visualizar Respostas - Pergunta 2'),
                ),
                ElevatedButton(
                  onPressed: () {
                    if (noOptionsSelected1 && noOptionsSelected2) {
                      showDialog(
                        context: context,
                        builder: (BuildContext context) {
                          return AlertDialog(
                            title: Text('Nenhuma resposta foi selecionada'),
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
                            title: Text('Respostas - Perguntas 1 e 2'),
                            content: Column(
                              crossAxisAlignment: CrossAxisAlignment.start,
                              mainAxisSize: MainAxisSize.min,
                              children: [
                                Text('Respostas - Pergunta 1:'),
                                if (selectedOptionsQuestion1[0])
                                  Text('- ${questions[0].options[0]}'),
                                if (selectedOptionsQuestion1[1])
                                  Text('- ${questions[0].options[1]}'),
                                if (selectedOptionsQuestion1[2])
                                  Text('- ${questions[0].options[2]}'),
                                SizedBox(height: 8),
                                Text('Respostas - Pergunta 2:'),
                                if (selectedOptionsQuestion2[0])
                                  Text('- ${questions[1].options[0]}'),
                                if (selectedOptionsQuestion2[1])
                                  Text('- ${questions[1].options[1]}'),
                                if (selectedOptionsQuestion2[2])
                                  Text('- ${questions[1].options[2]}'),
                              ],
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
                    }
                  },
                  style: ButtonStyle(
                    backgroundColor: MaterialStateProperty.all<Color>(Color(0xFF008080)),
                  ),
                  child: Text('Visualizar Respostas - Perguntas 1 e 2'),
                ),
              ],
            ),
          ],
        ),
      ),
      backgroundColor: Colors.white,
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: QuestionPage(),
  ));
}

```
<p align="right"><a href="#topo">Voltar ao Topo</p> 
