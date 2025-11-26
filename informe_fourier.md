# Explicacion del Codigo

El código implementa la Transformada Discreta de Fourier (DFT) a través de la clase TransformadaFourier, cuyo objetivo es convertir una señal del dominio del tiempo al dominio de la frecuencia. La función principal, dft, aplica la fórmula matemática estándar sumando las muestras de la señal ponderadas por exponenciales complejos (utilizando la librería cmath), lo que permite identificar qué frecuencias componen la señal original. El resultado es una lista de números complejos que representan el espectro de la señal.

  Además, el código incluye una función auxiliar para calcular la magnitud de estos valores complejos, lo que permite cuantificar la energía o intensidad de cada frecuencia presente. Es una implementación teórica directa, ideal para comprender los fundamentos del análisis espectral.

  ```python
  
import math
import cmath

class TransformadaFourier:
    def init(self, señal: list):
        """
        Inicializa la clase con una señal (lista de números).
        """
        self.señal = señal
        self.N = len(señal)
        self.transformada = None

    def dft(self) -> list:
        """
        Calcula la Transformada Discreta de Fourier (DFT) de la señal.
        """
        X = []
        for k in range(self.N):
            suma = 0
            for n in range(self.N):
                angulo = -2j * math.pi * k * n / self.N
                suma += self.señal[n] * cmath.exp(angulo)
            X.append(suma)
        self.transformada = X
        return X

    def abs_complejo_formula(z: complex) -> complex:
        """
        Calcula el valor absoluto de un número complejo y lo devuelve como complejo.
        """
        if isinstance(z, complex):
            a = z.real
            b = z.imag
            magnitud = math.sqrt(a*a + b*b)
            return complex(magnitud, 0)
        try:
            return complex(abs(z), 0)
        except Exception as e:
            raise TypeError(f"No se pudo calcular |z| para tipo {type(z)}: {e}")
  ```