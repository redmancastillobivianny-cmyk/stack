# stack
class Cuaderno:
    """Nodo que representa un cuaderno en la pila."""
    def __init__(self, numero: int):
        self.numero = numero
        self.siguiente = None

    def __repr__(self):
        return f"Cuaderno({self.numero})"

class PilaCuadernos:
    """Pila LIFO implementada con nodos enlazados."""
    def __init__(self):
        self.tope = None

    def esta_vacia(self) -> bool:
        return self.tope is None

    def apilar(self, numero: int):
        """Agrega un nuevo cuaderno en la parte superior."""
        nuevo_cuaderno = Cuaderno(numero)
        nuevo_cuaderno.siguiente = self.tope
        self.tope = nuevo_cuaderno

    def desapilar(self):
        """Retira y devuelve el cuaderno del tope. Si está vacía, no da error."""
        if self.esta_vacia():
            return None
        
        cuaderno_retirado = self.tope
        self.tope = self.tope.siguiente
        cuaderno_retirado.siguiente = None  # Rompe la referencia
        return cuaderno_retirado

    def peek(self):
        """Muestra el número del tope sin retirarlo."""
        if self.esta_vacia():
            return None
        return self.tope.numero

    def mostrar(self):
        """Recorre e imprime desde el tope hasta None."""
        actual = self.tope
        if actual is None:
            print("None")
            return

        elementos = []
        while actual is not None:
            elementos.append(str(actual.numero))
            actual = actual.siguiente
        
        print(" -> ".join(elementos) + " -> None")

# --- EJECUCIÓN EXACTA DE LA ACTIVIDAD ---

if __name__ == "__main__":
    pila = PilaCuadernos()

    # 1. Crear y agregar 1, 2, 3, 4 en ese orden
    for i in [1, 2, 3, 4]:
        pila.apilar(i)

    # 2. Mostrar contenido
    print("Contenido de la pila:")
    pila.mostrar()

    # 3. Peek sin eliminar
    print(f"\nCuaderno en el tope: {pila.peek()}")

    # 4. Desapilar uno y mostrar de nuevo
    retirado = pila.desapilar()
    if retirado:
        print(f"\nCuaderno retirado: {retirado.numero}")

    print("\nContenido de la pila después de desapilar:")
    pila.mostrar()
