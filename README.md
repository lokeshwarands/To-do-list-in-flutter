# To-do-list-in-flutter
import 'package:flutter/material.dart';

void main() => runApp(TodoList());

class TodoList extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'To-Do List App',
      home: TodoListPage(),
    );
  }
}

class TodoListPage extends StatefulWidget {
  @override
  _TodoListPageState createState() => _TodoListPageState();
}

class _TodoListPageState extends State<TodoListPage> {
  List<String> _todoList = [];
  String _newTodo = "";

  _addTodo() {
    setState(() {
      if (_newTodo.length > 0) {
        _todoList.add(_newTodo);
        _newTodo = "";
      }
    });
  }

  _deleteTodoItem(int index) {
    setState(() {
      _todoList.removeAt(index);
    });
  }

  Widget buildTodoItem(String todo, int index) {
    return Card(
      child: ListTile(
        title: Text(
          todo,
          style: TextStyle(
            fontSize: 20.0,
            fontWeight: FontWeight.bold,
          ),
        ),
        trailing: IconButton(
          icon: Icon(Icons.delete),
          onPressed: () => _deleteTodoItem(index),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        backgroundColor: Color.fromARGB(255, 247, 132, 39),
        title: Text("To-Do List App"),
      ),
      body: Column(
        children: <Widget>[
          Container(
            padding: EdgeInsets.symmetric(
              vertical: 24.0,
              horizontal: 12.0,
            ),
            child: TextField(
              decoration: InputDecoration(
                hintText: 'Add a new to-do item',
                border: OutlineInputBorder(),
              ),
              onChanged: (text) {
                _newTodo = text;
              },
              onSubmitted: (text) {
                _addTodo();
              },
            ),
          ),
          Expanded(
            child: ListView.builder(
              itemCount: _todoList.length,
              itemBuilder: (context, index) {
                return buildTodoItem(_todoList[index], index);
              },
            ),
          ),
        ],
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _addTodo,
        child: Icon(Icons.add),
      ),
    );
  }
}
