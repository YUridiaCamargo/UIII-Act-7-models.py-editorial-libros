# UIII-Act-7-models.py-editorial-libros
Sistema de Gestión de Editorial (Libros)
<img width="1710" height="826" alt="image" src="https://github.com/user-attachments/assets/d5fe3674-377f-4d79-9533-701602a7f97a" />





Aquí tienes **únicamente los modelos en Django (models.py)** según la información que proporcionaste, con **todas las relaciones correctamente declaradas** y usando nombres de campo adecuados para Django:

---

### 📌 **models.py — Grupo 40: Sistema de Gestión de Empresas de Limpieza**

```python
from django.db import models

class Cliente_Limpieza(models.Model):
    id_cliente = models.AutoField(primary_key=True)
    nombre_empresa = models.CharField(max_length=255)
    contacto_principal = models.CharField(max_length=100)
    email_contacto = models.EmailField(max_length=100)
    telefono_contacto = models.CharField(max_length=20)
    direccion_servicio = models.CharField(max_length=255)
    tipo_negocio = models.CharField(max_length=100)
    fecha_inicio_contrato = models.DateField()
    estado_contrato = models.CharField(max_length=50)
    frecuencia_servicio = models.CharField(max_length=50)

    def __str__(self):
        return self.nombre_empresa


class Servicio_Limpieza(models.Model):
    id_servicio = models.AutoField(primary_key=True)
    nombre_servicio = models.CharField(max_length=100)
    descripcion = models.TextField()
    costo_estandar = models.DecimalField(max_digits=10, decimal_places=2)
    duracion_estimada_horas = models.IntegerField()
    productos_usados = models.TextField()
    requiere_equipo_especial = models.BooleanField(default=False)
    categoria_servicio = models.CharField(max_length=50)

    def __str__(self):
        return self.nombre_servicio


class Empleado_Limpieza(models.Model):
    id_empleado = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    dni = models.CharField(max_length=20, unique=True)
    fecha_contratacion = models.DateField()
    salario_hora = models.DecimalField(max_digits=5, decimal_places=2)
    turno = models.CharField(max_length=50)
    telefono = models.CharField(max_length=20)
    email = models.EmailField(max_length=100)
    certificaciones_seguridad = models.TextField(blank=True)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"


class Programacion_Servicio(models.Model):
    id_programacion = models.AutoField(primary_key=True)
    id_cliente = models.ForeignKey(Cliente_Limpieza, on_delete=models.CASCADE)
    id_servicio = models.ForeignKey(Servicio_Limpieza, on_delete=models.CASCADE)
    fecha_programada = models.DateTimeField()
    hora_inicio = models.TimeField()
    hora_fin = models.TimeField()
    estado_servicio = models.CharField(max_length=50)
    observaciones_cliente = models.TextField(blank=True)
    id_empleado_asignado = models.ForeignKey(Empleado_Limpieza, on_delete=models.SET_NULL, null=True)

    def __str__(self):
        return f"Servicio {self.id_programacion} - {self.id_cliente.nombre_empresa}"


class Factura_Limpieza(models.Model):
    id_factura = models.AutoField(primary_key=True)
    id_cliente = models.ForeignKey(Cliente_Limpieza, on_delete=models.CASCADE)
    fecha_emision = models.DateField()
    monto_total = models.DecimalField(max_digits=10, decimal_places=2)
    estado_pago = models.CharField(max_length=50)
    metodo_pago = models.CharField(max_length=50)
    fecha_vencimiento = models.DateField()
    id_programacion_asociada = models.ForeignKey(Programacion_Servicio, on_delete=models.SET_NULL, null=True)
    impuestos_aplicados = models.DecimalField(max_digits=5, decimal_places=2)

    def __str__(self):
        return f"Factura #{self.id_factura}"


class Material_Limpieza(models.Model):
    id_material = models.AutoField(primary_key=True)
    nombre_material = models.CharField(max_length=255)
    descripcion = models.TextField()
    stock_actual = models.IntegerField()
    fecha_caducidad = models.DateField()
    id_proveedor = models.IntegerField()  # No se especificó modelo proveedor
    costo_unitario = models.DecimalField(max_digits=10, decimal_places=2)
    tipo_material = models.CharField(max_length=50)
    ubicacion_almacen = models.CharField(max_length=100)

    def __str__(self):
        return self.nombre_material


class Uso_Material(models.Model):
    id_uso = models.AutoField(primary_key=True)
    id_programacion = models.ForeignKey(Programacion_Servicio, on_delete=models.CASCADE)
    id_material = models.ForeignKey(Material_Limpieza, on_delete=models.CASCADE)
    cantidad_usada = models.DecimalField(max_digits=8, decimal_places=2)
    fecha_registro = models.DateTimeField()
    id_empleado_registro = models.ForeignKey(Empleado_Limpieza, on_delete=models.SET_NULL, null=True)
    comentarios_uso = models.TextField(blank=True)

    def __str__(self):
        return f"Uso #{self.id_uso}"
```

---

### ✔️ Incluido correctamente

| Característica                              | Estado |
| ------------------------------------------- | ------ |
| Campos y tipos según tu tabla               | ✔️     |
| Relaciones ManyToOne con ForeignKey         | ✔️     |
| Nombres de clave primaria manuales (`id_*`) | ✔️     |
| Compatibilidad con Django ORM               | ✔️     |
| `__str__` para facilitar administración     | ✔️     |

---

Si quieres, también puedo entregarte:

✅ Admin.py completo
✅ Forms y Vistas CRUD
✅ URLs organizadas
✅ Datos de prueba (fixtures)
📌 Incluso todo empaquetado en un proyecto Django listo para correr

¿Quieres que te genere también **el diagrama relacional** o **el script SQL para la base de datos**?
