# ListView

<br id="topo">

<div align="center">

<img src = 'https://github.com/bruno-pisciotta281/flutter_dart-studys/blob/Exercício-02/exercício%2002.jpeg'  width="500">

</div>

<br>
- Códigos para rodar a aplicação (feita utilizando a plataforma (https://zapp.run)


```bash


import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: LoginPage(),
    theme: ThemeData(
      primaryColor: Color(0xFF008080),
      scaffoldBackgroundColor: Colors.white,
      textTheme: TextTheme(
        headline6: TextStyle(color: Colors.white, fontSize: 24.0),
        bodyText2: TextStyle(color: Color(0xFF008080)),
      ),
    ),
  ));
}

class LoginPage extends StatefulWidget {
  @override
  _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final TextEditingController nameController = TextEditingController();
  final TextEditingController emailController = TextEditingController();
  String errorMessage = '';

  void login() {
    String name = nameController.text;
    String email = emailController.text;
    if (name.isEmpty || email.isEmpty) {
      showDialog(
        context: context,
        builder: (BuildContext context) {
          return AlertDialog(
            title: Text('Erro de Login'),
            content: Text('Por favor, preencha todos os campos.'),
            actions: [
              TextButton(
                onPressed: () {
                  Navigator.of(context).pop();
                },
                child: Text('OK'),
              ),
            ],
          );
        },
      );
    } else {
      Navigator.push(
        context,
        MaterialPageRoute(
          builder: (context) => ProductListPage(),
        ),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Container(
              width: 150,
              height: 150,
              decoration: BoxDecoration(
                color: Color(0xFF008080),
                shape: BoxShape.circle,
              ),
              child: Center(
                child: Icon(
                  Icons.account_circle,
                  size: 100,
                  color: Colors.white,
                ),
              ),
            ),
            SizedBox(height: 32.0),
            TextField(
              controller: nameController,
              decoration: InputDecoration(
                labelText: 'Nome',
                filled: true,
                fillColor: Color(0xFF008080),
                labelStyle: TextStyle(color: Colors.white),
              ),
              style: TextStyle(color: Colors.white),
            ),
            SizedBox(height: 16.0),
            TextField(
              controller: emailController,
              decoration: InputDecoration(
                labelText: 'Email',
                filled: true,
                fillColor: Color(0xFF008080),
                labelStyle: TextStyle(color: Colors.white),
              ),
              style: TextStyle(color: Colors.white),
            ),
            SizedBox(height: 16.0),
            ElevatedButton(
              onPressed: login,
              child: Text('Login'),
              style: ElevatedButton.styleFrom(
                primary: Color(0xFF008080),
              ),
            ),
            Text(
              errorMessage,
              style: TextStyle(
                color: Colors.red,
              ),
            ),
          ],
        ),
      ),
    );
  }
}

class Product {
  final String name;
  final String description;
  int quantity;

  Product({required this.name, required this.description, this.quantity = 1});
}

class ProductListPage extends StatelessWidget {
  final List<Product> products = [
    Product(name: 'Produto 1', description: 'Descrição do Produto 1'),
    Product(name: 'Produto 2', description: 'Descrição do Produto 2'),
    Product(name: 'Produto 3', description: 'Descrição do Produto 3'),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          'Lista de Produtos',
          style: TextStyle(backgroundColor: Color(0xFF008080)),
        ),
        backgroundColor: Color(0xFF008080),
      ),
      body: ListView.builder(
        itemCount: products.length,
        itemBuilder: (BuildContext context, int index) {
          Product product = products[index];
          return ListTile(
            title: Text(
              product.name,
              style: TextStyle(color: Color(0xFF008080)),
            ),
            subtitle: Text(
              product.description,
              style: TextStyle(color: Color(0xFF008080)),
            ),
            onTap: () {
              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => ProductDetailsPage(product: product),
                ),
              );
            },
          );
        },
      ),
    );
  }
}

class ProductDetailsPage extends StatefulWidget {
  final Product product;

  ProductDetailsPage({required this.product});

  @override
  _ProductDetailsPageState createState() => _ProductDetailsPageState();
}

class _ProductDetailsPageState extends State<ProductDetailsPage> {
  int _quantity = 1;

  void _increaseQuantity() {
    setState(() {
      _quantity++;
    });
  }

  void _decreaseQuantity() {
    if (_quantity > 1) {
      setState(() {
        _quantity--;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          'Detalhes do Produto',
          style: TextStyle(backgroundColor: Color(0xFF008080)),
        ),
        backgroundColor: Color(0xFF008080),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text(
              'Nome: ${widget.product.name}',
              style: TextStyle(fontSize: 18.0, fontWeight: FontWeight.bold, backgroundColor: Colors.white),
            ),
            SizedBox(height: 8.0),
            Text(
              'Descrição: ${widget.product.description}',
              style: TextStyle(fontSize: 16.0),
            ),
            SizedBox(height: 16.0),
            Text(
              'Quantidade: $_quantity',
              style: TextStyle(fontSize: 16.0),
            ),
            Row(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                IconButton(
                  onPressed: _decreaseQuantity,
                  icon: Icon(Icons.remove),
                ),
                IconButton(
                  onPressed: _increaseQuantity,
                  icon: Icon(Icons.add),
                ),
              ],
            ),
            SizedBox(height: 16.0),
            ElevatedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => SuccessPage(),
                  ),
                );
              },
              child: Text('Comprar'),
              style: ElevatedButton.styleFrom(
                primary: Color(0xFF008080),
              ),
            ),
          ],
        ),
      ),
    );
  }
}

class SuccessPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          'Vendido com Sucesso',
          style: TextStyle(backgroundColor: Color(0xFF008080)),
        ),
        backgroundColor: Color(0xFF008080),
      ),
      body: Center(
        child: Column(
          children: [
            Image.asset(
              'assets/logo.png',
              width: 150,
              height: 150,
            ),
            Text(
              'Vendido com sucesso!',
              style: TextStyle(fontSize: 24.0),
            ),
          ],
        ),
      ),
    );
  }
}


```
<p align="right"><a href="#topo">Voltar ao Topo</p> 
