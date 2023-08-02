# Factura-Nv1.
Un pequeño programa de facturación en base beta 0.1 en el programa de Java Main

Lo primero seria un class y luego un Main Class:
JAVA CLASS:
package com.mycompany.phase_1;
public class Cliente {
 private String nombre;
 private int telefono;
 private String servicio;
 private int cantidad;
 private double costo;
 private double total;
 public Cliente(String nombre, int telefono, String servicio, int cantidad, double costo)
{
 this.nombre = nombre;
 this.telefono = telefono;
 this.servicio = servicio;
 this.cantidad = cantidad;
 this.costo = costo;
 this.total = cantidad * costo;
 }
 public String getNombre() {
 return nombre;
 }
 public int getTelefono() {
 return telefono;
 }
 public String getServicio() {
 return servicio;
 }
 public int getCantidad() {
 return cantidad;
 }
 public double getCosto() {
 return costo;
 }
 public double getTotal() {
 return total;
 }
} 


JAVA MAIN:
import javax.swing.JOptionPane;
public class TA_3M {
 public static void main(String[] args) {
 int numClientes = 0;
 while (numClientes <= 0) {
 try {
 numClientes = Integer.parseInt(JOptionPane.showInputDialog("Ingrese el
número de clientes (al menos 1):"));
 if (numClientes <= 0) {
 throw new Exception("ERROR, ingrese un número de clientes válido");
 }
 } catch (NumberFormatException e) {
 JOptionPane.showMessageDialog(null, "ERROR, ingrese un número
válido");
 } catch (Exception e) {
 JOptionPane.showMessageDialog(null, e.getMessage());
 }
 }
 Cliente[] clientes = new Cliente[numClientes];
 for (int i = 0; i < numClientes; i++) {
 String nombre = JOptionPane.showInputDialog("Ingrese el nombre del cliente "
+ (i + 1));
 int telefono;
 do {
 telefono = Integer.parseInt(JOptionPane.showInputDialog("Ingrese el numero
de telefono"));
 if (telefono < 900000000 || telefono > 1000000000) {
 JOptionPane.showMessageDialog(null, "ERROR, ingrese un numero de
telefono valido");
 }
 } while (telefono < 900000000 || telefono > 1000000000);
 // Crear una tabla de selección para el servicio
 String[] servicios = {
 "Consulta Veterinaria",
 "Vacunación",
 "Cirugía Veterinaria",
 "Hospitalización",
 "Laboratorio y Diagnóstico",
 "Imagenología",
 "Limpieza y Desinfección",
 "Peluquería y Estética Animal",
 "Alimentación y Nutrición",
 "Tienda de Mascotas",
 "Guardería y Paseo de Perros",
 "Adopción Responsable"
 };
 String servicioSeleccionado = (String) JOptionPane.showInputDialog(
 null,
 "Seleccione el servicio para el cliente " + (i + 1) + ":",
 "Selección de Servicio",
 JOptionPane.PLAIN_MESSAGE,
 null,
 servicios,
 servicios[0]
 );
 String servicio = "";
 for (String s : servicios) {
TALLER DE PROGRAMACION
 if (servicioSeleccionado.equals(s)) {
 servicio = s;
 break;
 }
 }
 int cantidad = Integer.parseInt(JOptionPane.showInputDialog("Ingrese la
cantidad de servicios"));
 double costo = Double.parseDouble(JOptionPane.showInputDialog("Ingrese el
costo del servicio:"));
 clientes[i] = new Cliente(nombre, telefono, servicio, cantidad, costo);
 }
 StringBuilder factura = new StringBuilder();
 factura.append("FACTURA\n");
 factura.append("----------------\n");
 for (Cliente cliente : clientes) {
 factura.append("NOMBRE: ").append(cliente.getNombre()).append("\n");
 factura.append("TELEFONO: ").append(cliente.getTelefono()).append("\n");
 factura.append("DESCRIPCION: ").append(cliente.getServicio()).append("\n");
 factura.append("CANTIDAD: ").append(cliente.getCantidad()).append("\n");
 factura.append("COSTO: ").append(cliente.getCosto()).append("\n");
 factura.append("TOTAL: ").append(cliente.getTotal()).append("\n");
 factura.append("----------------\n");
 }
 JOptionPane.showMessageDialog(null, factura.toString());
 }
}
