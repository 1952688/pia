# pia
from collections import namedtuple
import datetime

Detalle = namedtuple("Detalle", ("clave_articulo", "cantidad", "precio_unitario"))
lista_detalle = list()
clave = 1
acumulado = 0

cliente = input("Cliente al que se le realizó la venta: ")
while True:
    try:
        fecha_str = input("Fecha de la venta en formato (dd/mm/aaaa): ")
        fecha = datetime.datetime.strptime(fecha_str, "%d/%m/%Y").date()
    except ValueError:
        print("El valor de la fecha que fue proporcionado no puede ser procesado")
        continue
    except Exception:
        print("Se ha presentado una excepción")
        break
    else:
        while clave != 0:
            clave = int(input("\nIndique la clave del artículo <0 para salir>: "))
            
            if clave == 0:
                break
            else:
                descripcion=input("describa el producto: ")
                cantidad = int(input("Indique la cantidad de artículos: "))
                precio_unitario = float(input("Indique el precio unitario para este artículo: "))
                detalle = Detalle(clave, cantidad, precio_unitario)
                lista_detalle.append(detalle)

                acumulado += (cantidad * precio_unitario )
                iva =(acumulado*.16 )
                precio_total= (iva + acumulado)
        
        if acumulado == 0:
            print("\nLa venta no contiene detalle alguno, por lo tanto no se registra")
        else:
            print(f"\nDescripcion del producto: {descripcion}")
            print(f"\nEl total de la venta antes de impuestos es de ${acumulado:.2f}")
            print(f"\nEl total con iva es: ${iva}")
            print(f"\nVenta realizada a {cliente} con fecha de {fecha}")
            print(f"\nPrecio total:{precio_total}")
            print("-" * 55)
            print("Clave del artículo\tCantidad\tPrecio Unitario")
            for detalle in lista_detalle:
                print(f"{detalle.clave_articulo}\t\t\t{detalle.cantidad}\t\t${detalle.precio_unitario:.2f}")
            print("-" * 55)
                
    
    break
