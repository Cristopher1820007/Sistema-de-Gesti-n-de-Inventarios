# Sistema-de-Gesti-n-de-Inventarios
Desarrollar un sistema de gestión de inventarios simple para una tienda, que permita añadir, actualizar, eliminar y buscar productos utilizando una estructura de datos personalizada
class Producto:
    def __init__(self, id_producto, nombre, cantidad, precio):
        self.id_producto = id_producto
        self.nombre = nombre
        self.cantidad = cantidad
        self.precio = precio

    def get_id(self):
        return self.id_producto

    def get_nombre(self):
        return self.nombre

    def get_cantidad(self):
        return self.cantidad

    def get_precio(self):
        return self.precio

    def set_nombre(self, nombre):
        self.nombre = nombre

    def set_cantidad(self, cantidad):
        self.cantidad = cantidad

    def set_precio(self, precio):
        self.precio = precio

    def __str__(self):
        return f"ID: {self.id_producto} | Nombre: {self.nombre} | Cantidad: {self.cantidad} | Precio: ${self.precio:.2f}"


class Inventario:
    def __init__(self):
        self.productos = []

    def agregar_producto(self, producto):
        if any(p.get_id() == producto.get_id() for p in self.productos):
            print(" Error: El ID ya existe en el inventario.")
            return
        self.productos.append(producto)
        print(" Producto agregado correctamente.")

    def eliminar_producto(self, id_producto):
        for p in self.productos:
            if p.get_id() == id_producto:
                self.productos.remove(p)
                print(" Producto eliminado.")
                return
        print(" Producto no encontrado.")

    def actualizar_producto(self, id_producto, cantidad=None, precio=None):
        for p in self.productos:
            if p.get_id() == id_producto:
                if cantidad is not None:
                    p.set_cantidad(cantidad)
                if precio is not None:
                    p.set_precio(precio)
                print(" Producto actualizado.")
                return
        print(" Producto no encontrado.")

    def buscar_por_nombre(self, nombre):
        resultados = [p for p in self.productos if nombre.lower() in p.get_nombre().lower()]
        if resultados:
            print("\n Resultados de búsqueda:")
            for p in resultados:
                print(p)
        else:
            print(" No se encontraron productos con ese nombre.")

    def mostrar_todos(self):
        if not self.productos:
            print(" El inventario está vacío.")
        else:
            print("\n Inventario completo:")
            for p in self.productos:
                print(p)

    def mostrar_ids_nombres(self):
        if not self.productos:
            print(" El inventario está vacío.")
        else:
            print("\n Lista de productos disponibles:")
            for p in self.productos:
                print(f"ID: {p.get_id()} - Nombre: {p.get_nombre()}")


def menu():
    inventario = Inventario()

    while True:
        print("\n" + "="*25)
        print("  MENÚ DE INVENTARIO")
        print("="*25)
        print("1. Agregar producto")
        print("2. Eliminar producto")
        print("3. Actualizar producto")
        print("4. Buscar producto por nombre")
        print("5. Mostrar todos los productos")
        print("6. Mostrar lista de IDs y nombres")
        print("7. Salir")

        opcion = input("\nSeleccione una opción: ")

        if opcion == "1":
            try:
                id_producto = input("Ingrese ID: ")
                nombre = input("Ingrese nombre: ")
                cantidad = int(input("Ingrese cantidad: "))
                precio = float(input("Ingrese precio: "))
                inventario.agregar_producto(Producto(id_producto, nombre, cantidad, precio))
            except ValueError:
                print(" Error: Cantidad y precio deben ser números.")

        elif opcion == "2":
            inventario.mostrar_ids_nombres()
            id_producto = input("Ingrese ID del producto a eliminar: ")
            inventario.eliminar_producto(id_producto)

        elif opcion == "3":
            inventario.mostrar_ids_nombres()
            id_producto = input("Ingrese ID del producto a actualizar: ")
            c_input = input("Nueva cantidad (vacío para no cambiar): ")
            p_input = input("Nuevo precio (vacío para no cambiar): ")
            
            try:
                cantidad = int(c_input) if c_input else None
                precio = float(p_input) if p_input else None
                inventario.actualizar_producto(id_producto, cantidad, precio)
            except ValueError:
                print(" Error: Los valores ingresados deben ser numéricos.")

        elif opcion == "4":
            nombre = input("Ingrese nombre a buscar: ")
            inventario.buscar_por_nombre(nombre)

        elif opcion == "5":
            inventario.mostrar_todos()

        elif opcion == "6":
            inventario.mostrar_ids_nombres()

        elif opcion == "7":
            print(" Saliendo del sistema... ¡Hasta luego!")
            break
        else:
            print(" Opción inválida, intente nuevamente.")

if __name__ == "__main__":
    menu()
