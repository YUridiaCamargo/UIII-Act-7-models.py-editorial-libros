# UIII-Act-7-models.py-editorial-libros
Sistema de Gestión de Editorial (Libros)
<img width="1174" height="769" alt="image" src="https://github.com/user-attachments/assets/1e95d424-b3c2-446e-8202-2439ebbe9df4" />




---

# ✅ **models.py (Django)**

```python
from django.db import models


class AutorEditorial(models.Model):
    id_autor = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    nacionalidad = models.CharField(max_length=50)
    fecha_nacimiento = models.DateField()
    biografia = models.TextField()
    email = models.CharField(max_length=100)
    sitio_web = models.CharField(max_length=255, blank=True, null=True)
    fecha_fallecimiento = models.DateField(blank=True, null=True)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"


class GeneroLiterario(models.Model):
    id_genero = models.AutoField(primary_key=True)
    nombre_genero = models.CharField(max_length=50)
    descripcion = models.TextField()
    es_ficcion = models.BooleanField()
    epoca_popular = models.CharField(max_length=50)
    publico_objetivo = models.CharField(max_length=100)

    def __str__(self):
        return self.nombre_genero


class Editor(models.Model):
    id_editor = models.AutoField(primary_key=True)
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    email = models.CharField(max_length=100)
    telefono = models.CharField(max_length=20)
    fecha_contratacion = models.DateField()
    salario = models.DecimalField(max_digits=10, decimal_places=2)
    especialidad_genero = models.CharField(max_length=100)
    departamento = models.CharField(max_length=50)
    dni = models.CharField(max_length=20)

    def __str__(self):
        return f"{self.nombre} {self.apellido}"


class LibroEditorial(models.Model):
    id_libro = models.AutoField(primary_key=True)
    titulo = models.CharField(max_length=255)
    autor_principal = models.ForeignKey(AutorEditorial, on_delete=models.CASCADE)
    isbn = models.CharField(max_length=13)
    fecha_publicacion = models.DateField()
    num_paginas = models.IntegerField()
    genero = models.ForeignKey(GeneroLiterario, on_delete=models.CASCADE)
    precio_tapa = models.DecimalField(max_digits=10, decimal_places=2)
    stock_almacen = models.IntegerField()
    editor = models.ForeignKey(Editor, on_delete=models.CASCADE)
    estado_publicacion = models.CharField(max_length=50)
    formato = models.CharField(max_length=50)

    def __str__(self):
        return self.titulo


class Distribuidor(models.Model):
    id_distribuidor = models.AutoField(primary_key=True)
    nombre_distribuidor = models.CharField(max_length=100)
    contacto_principal = models.CharField(max_length=100)
    telefono = models.CharField(max_length=20)
    email = models.CharField(max_length=100)
    direccion_almacen = models.CharField(max_length=255)
    pais_distribucion = models.CharField(max_length=50)
    tipo_distribucion = models.CharField(max_length=50)

    def __str__(self):
        return self.nombre_distribuidor


class EnvioLibros(models.Model):
    id_envio = models.AutoField(primary_key=True)
    libro = models.ForeignKey(LibroEditorial, on_delete=models.CASCADE)
    distribuidor = models.ForeignKey(Distribuidor, on_delete=models.CASCADE)
    fecha_envio = models.DateTimeField()
    cantidad_enviada = models.IntegerField()
    costo_envio = models.DecimalField(max_digits=10, decimal_places=2)
    estado_envio = models.CharField(max_length=50)
    fecha_recepcion_esperada = models.DateField()
    numero_seguimiento = models.CharField(max_length=50)

    def __str__(self):
        return f"Envío {self.id_envio} - {self.libro.titulo}"


class ContratoAutor(models.Model):
    id_contrato = models.AutoField(primary_key=True)
    libro = models.ForeignKey(LibroEditorial, on_delete=models.CASCADE)
    autor_principal = models.ForeignKey(AutorEditorial, on_delete=models.CASCADE)
    fecha_firma = models.DateField()
    porcentaje_regalias = models.DecimalField(max_digits=5, decimal_places=2)
    monto_adelanto = models.DecimalField(max_digits=10, decimal_places=2)
    fecha_fin_contrato = models.DateField()
    clausulas_especiales = models.TextField()
    id_agente_literario = models.IntegerField()

    def __str__(self):
        return f"Contrato {self.id_contrato} - {self.autor_principal}"
```

---

¿Deseas alguna de estas opciones?

