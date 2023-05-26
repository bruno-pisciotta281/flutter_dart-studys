# SIMULADO - Questões de Prova
<br id="topo">

<div align="center">

<img src = 'https://github.com/bruno-pisciotta281/flutter_dart-studys/blob/SIMULADO/Simulado.png'  width="500">

<p>OBS: Como não haviam perguntas e nem respostas no exemplo criei um padrão e fiz com que as questões corretas fossem aquelas que contiam o número 3 e letras vogais, enquanto as outras estão todas erradas.</p>
  
</div>

<br>
- Códigos para rodar a aplicação (feita utilizando a plataforma (https://zapp.run)


```bash
import 'package:flutter/material.dart';

class Question {
  final String title;
  final List<String> options;
  final int correctAnswer;

  Question({
    required this.title,
    required this.options,
    required this.correctAnswer,
  });
}

class QuizApp extends StatefulWidget {
  @override
  _QuizAppState createState() => _QuizAppState();
}

class _QuizAppState extends State<QuizApp> {
  List<Question> questions = [
    Question(
      title: 'Pergunta 1',
      options: ['Opção 1', 'Opção 2', 'Opção 3'],
      correctAnswer: 2,
    ),
    Question(
      title: 'Pergunta 2',
      options: ['Opção A', 'Opção B', 'Opção C'],
      correctAnswer: 2,
    ),
    Question(
      title: 'Pergunta 3',
      options: ['Opção X', 'Opção Y', 'Opção Z'],
      correctAnswer: 0,
    ),
    Question(
      title: 'Pergunta 4',
      options: ['Opção M', 'Opção N', 'Opção O'],
      correctAnswer: 0,
    ),
    Question(
      title: 'Pergunta 5',
      options: ['Opção P', 'Opção Q', 'Opção R'],
      correctAnswer: 0,
    ),
  ];

  List<int?> selectedAnswers = List.filled(5, null);
  bool isQuizSubmitted = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('SIMULADO: "Avaliação de Moblie II" - Bruno Pisciotta'),
        backgroundColor: Color(0xFF008080),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Responda as questões:',
              style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold),
            ),
            SizedBox(height: 16),
            Expanded(
              child: ListView.builder(
                itemCount: questions.length,
                itemBuilder: (context, index) {
                  return QuestionWidget(
                    question: questions[index],
                    index: index,
                    selectedAnswer: selectedAnswers[index],
                    isQuizSubmitted: isQuizSubmitted,
                    onAnswerSelected: (answer) {
                      setState(() {
                        selectedAnswers[index] = answer;
                      });
                    },
                  );
                },
              ),
            ),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: isQuizSubmitted ? null : submitQuiz,
              style: ButtonStyle(
                backgroundColor: MaterialStateProperty.all(Color(0xFF008080)),
              ),
              child: Text(
                'Enviar',
                style: TextStyle(color: Colors.white),
              ),
            ),
          ],
        ),
      ),
    );
  }

  void submitQuiz() {
    setState(() {
      isQuizSubmitted = true;
    });
  }
}

class QuestionWidget extends StatelessWidget {
  final Question question;
  final int index;
  final int? selectedAnswer;
  final bool isQuizSubmitted;
  final Function(int) onAnswerSelected;

  QuestionWidget({
    required this.question,
    required this.index,
    required this.selectedAnswer,
    required this.isQuizSubmitted,
    required this.onAnswerSelected,
  });

  Color getBackgroundColor(int optionIndex) {
    if (isQuizSubmitted) {
      final bool isCorrect =
          optionIndex == question.correctAnswer && question.title.contains('3') && containsVowel(question.options[optionIndex]);
      final bool isSelected = optionIndex == selectedAnswer;
      return isSelected ? (isCorrect ? Colors.green : Colors.red) : (isCorrect ? Colors.green : Colors.white);
    }
    return Colors.white;
  }

  Color getTextColor(int optionIndex) {
    if (isQuizSubmitted) {
      final bool isCorrect =
          optionIndex == question.correctAnswer && question.title.contains('3') && containsVowel(question.options[optionIndex]);
      final bool isSelected = optionIndex == selectedAnswer;
      return isSelected ? Colors.white : (isCorrect ? Colors.white : Colors.black);
    }
    return Colors.black;
  }

  bool containsVowel(String option) {
    final vowels = ['A', 'E', 'I', 'O', 'U'];
    for (var vowel in vowels) {
      if (option.toUpperCase().contains(vowel)) {
        return true;
      }
    }
    return false;
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        Text(
          question.title,
          style: TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
        ),
        SizedBox(height: 8),
        Column(
          children: List.generate(
            question.options.length,
            (optionIndex) => GestureDetector(
              onTap: () {
                if (!isQuizSubmitted) {
                  onAnswerSelected(optionIndex);
                }
              },
              child: Container(
                decoration: BoxDecoration(
                  color: getBackgroundColor(optionIndex),
                  border: Border.all(color: Colors.black),
                  borderRadius: BorderRadius.circular(8.0),
                ),
                margin: EdgeInsets.symmetric(vertical: 4),
                child: ListTile(
                  leading: Radio<int>(
                    value: optionIndex,
                    groupValue: selectedAnswer,
                    onChanged: (value) {
                      if (!isQuizSubmitted) {
                        onAnswerSelected(value!);
                      }
                    },
                  ),
                  title: Text(
                    question.options[optionIndex],
                    style: TextStyle(color: getTextColor(optionIndex)),
                  ),
                ),
              ),
            ),
          ),
        ),
        SizedBox(height: 16),
      ],
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: QuizApp(),
  ));
}


```
<p align="right"><a href="#topo">Voltar ao Topo</p> 
