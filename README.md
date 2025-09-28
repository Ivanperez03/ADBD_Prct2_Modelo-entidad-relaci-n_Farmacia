# Modelo Entidad-Relación: Farmacia

Este documento describe el modelo entidad/relación diseñado para el sistema de gestión de una farmacia.  
Se incluyen descripciones de entidades, atributos, relaciones, cardinalidades y restricciones semánticas.

---

## 📦 Entidades y atributos

### **Medicamento**
- **Atributos:**
  - `Codigo` (🔑, identificador único del medicamento).
  - `Nombre` (ej: *Paracetamol*).
  - `TipoForma` (ej: *comprimido, jarabe, pomada*).
  - `Stock` (número de unidades disponibles, ej: *150*).
  - `Vendidas` (número de unidades ya vendidas).
  - `Precio` (valor monetario, ej: *4.50 €*).

### **Familia**
- **Atributos:**
  - `Codigo` (🔑 identificador de la familia).
  - `TipoEnfermedades` (ej: *Antiinflamatorios, Analgésicos*).

### **Laboratorio**
- **Atributos:**
  - `Codigo` (🔑 identificador del laboratorio).
  - `Nombre` (ej: *Pfizer*).
  - `Telefono` (ej: *922123456*).
  - `Direccion` (ej: *Calle Salud, 25*).
  - `Fax` (opcional).
  - `Contacto` (persona responsable, ej: *Ana Ramos*).

### **Cliente**

### **Cliente_credito** (subtipo de Cliente)
- **Atributos adicionales:**
  - `ID` (heredado).
  - `DatosBancarios` (IBAN, banco).
  - `Fechas` (fecha de pago de las compras).
  
---

## 🔗 Relaciones y cardinalidades

### **pertenece** (Medicamento – Familia)
- Cada **Medicamento** pertenece a **exactamente una** familia.  
- Una **Familia** puede tener **varios** medicamentos.  
- **Cardinalidad:** (1,N) Medicamento – (1,1) Familia.

### **provee** (Medicamento – Laboratorio)
- Cada **Medicamento** puede ser provisto por **un laboratorio**.  
- Un **Laboratorio** puede proveer **muchos medicamentos**.  
- **Cardinalidad:** (1,N) Medicamento – (1,N) Laboratorio.

### **compra** (Cliente – Medicamento)
- Cada **Cliente** puede comprar **varios medicamentos**.  
- Cada **Medicamento** puede ser adquirido en varias compras.  
- Se incluyen atributos de la relación: `Fecha` y `Unidades`.  
- **Cardinalidad:** (1,N) Cliente – (1,N) Medicamento.

### **Venta** (Medicamento)
- Especialización en dos subtipos:
  - `VentaLibre`
  - `RecetaMedica`
- **Restricción:** Disjunta y total (todo medicamento debe ser uno de los dos tipos).

### **ISA Cliente** (Cliente)
- Especialización en dos subtipos:
  - `Cliente_credito`
  - Cliente sin crédito (implícito).
- **Jerarquia exlusiva y total**

---

## ⚖️ Restricciones semánticas

1. **Medicamento – Familia**: cada medicamento debe clasificarse en una única familia de enfermedades.  
2. **Medicamento – Tipo**: todo medicamento es **VentaLibre** o **RecetaMedica**, nunca ambos.  
3. **Cliente – Crédito**: un cliente puede ser **Cliente_credito**
4. **Unidades en compra** deben ser un número entero positivo.  
5. **Precio** de medicamento debe ser un valor mayor que cero.  

---
