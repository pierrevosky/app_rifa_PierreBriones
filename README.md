# app_rifa_PierreBriones
Aplicación móvil desarrollada en Flutter que simula una rifa digital. Permite visualizar 20 números con estados disponibles o reservados, seleccionar un número y confirmar su reserva mediante una interfaz interactiva.
# App de Rifa Flutter

Aplicación móvil desarrollada en Flutter que simula una rifa digital.

## Funcionalidades
- Lista de números del 1 al 20
- Estado disponible y reservado
- Selección de números
- Confirmación de reserva

## Tecnologías
- Flutter
- Dart

## Codigo 
import 'package:flutter/material.dart';

void main() {
  runApp(const MyApp());
}

class Numero {
  final int valor;
  bool reservado;

  Numero(this.valor, {this.reservado = false});
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'App Rifa',
      home: const HomeScreen(),
    );
  }
}

class HomeScreen extends StatelessWidget {
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Rifa Digital')),
      body: Center(
        child: ElevatedButton(
          child: const Text('Ver números'),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (_) => const ListaScreen()),
            );
          },
        ),
      ),
    );
  }
}

class ListaScreen extends StatefulWidget {
  const ListaScreen({super.key});

  @override
  State<ListaScreen> createState() => _ListaScreenState();
}

class _ListaScreenState extends State<ListaScreen> {
  List<Numero> numeros =
  List.generate(20, (index) => Numero(index + 1));

  void reservarNumero(Numero numero) {
    if (!numero.reservado) {
      setState(() {
        numero.reservado = true;
      });

      showDialog(
        context: context,
        builder: (_) => AlertDialog(
          title: const Text('Reserva confirmada'),
          content: Text('Número ${numero.valor} reservado'),
          actions: [
            TextButton(
              onPressed: () => Navigator.pop(context),
              child: const Text('OK'),
            )
          ],
        ),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Lista de números')),
      body: GridView.builder(
        gridDelegate: const SliverGridDelegateWithFixedCrossAxisCount(
          crossAxisCount: 4,
        ),
        itemCount: numeros.length,
        itemBuilder: (context, index) {
          final num = numeros[index];

          return GestureDetector(
            onTap: () => reservarNumero(num),
            child: Card(
              color: num.reservado ? Colors.red : Colors.green,
              child: Center(
                child: Text(
                  num.valor.toString().padLeft(2, '0'),
                  style: const TextStyle(fontSize: 20, color: Colors.white),
                ),
              ),
            ),
          );
        },
      ),
    );
  }
}


app.rifa.iml

<?xml version="1.0" encoding="UTF-8"?>
<module type="JAVA_MODULE" version="4">
  <component name="NewModuleRootManager" inherit-compiler-output="true">
    <exclude-output />
    <content url="file://$MODULE_DIR$">
      <sourceFolder url="file://$MODULE_DIR$/lib" isTestSource="false" />
      <sourceFolder url="file://$MODULE_DIR$/test" isTestSource="true" />
      <excludeFolder url="file://$MODULE_DIR$/.dart_tool" />
      <excludeFolder url="file://$MODULE_DIR$/.idea" />
      <excludeFolder url="file://$MODULE_DIR$/build" />
      <excludeFolder url="file://$MODULE_DIR$/.pub" />
    </content>
    <orderEntry type="sourceFolder" forTests="false" />
    <orderEntry type="library" name="Dart SDK" level="project" />
    <orderEntry type="library" name="Flutter Plugins" level="project" />
    <orderEntry type="library" name="Dart Packages" level="project" />
  </component>
</module>
