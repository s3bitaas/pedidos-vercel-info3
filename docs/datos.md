# Práctica 6: almacenes, entidades y diccionario inicial

## De almacenes a entidades

| Almacén del DFD | Qué guarda (una oración) | Entidad candidata | Identificador |
|---|---|---|---|
| D1 Clientes | Las personas que realizan pedidos y sus datos de contacto. | Cliente | @id_cliente |
| D2 Pedidos | Los pedidos realizados por los clientes, su estado y descuento. | Pedido | @id_pedido |
| D3 Detalle de pedidos | Los productos o servicios incluidos en cada pedido, con cantidad y precio. | DetallePedido | @id_detalle |
| D4 Productos y servicios | El catálogo de productos o servicios que pueden incluirse en un pedido. | ProductoServicio | @id_producto |

**Decisión:** DetallePedido une a Pedido con ProductoServicio y además tiene datos propios
(cantidad y precioUnitario), así que será una entidad asociativa en el modelo E-R.

## Diccionario de datos

### Almacenes

Pedido = @id_pedido + @id_cliente + estado + descuento + {id_detalle}

DetallePedido = @id_detalle + @id_pedido + @id_producto + cantidad + precioUnitario

### Flujos que cruzan la frontera del sistema

Solicitud de pedido = @id_cliente + {id_producto + cantidad} + (descuento)
*flujo que entra del Cliente*

Comprobante de pedido = @id_pedido + estado + total + fecha_entrega
*flujo que sale al Cliente*

### Datos con estados o categorías

estado = ["registrado" | "en_preparacion" | "listo" | "entregado"]

### Definiciones de datos

Cliente = @id_cliente + nombre + telefono + (email)

ProductoServicio = @id_producto + nombre_producto + precio_unitario

nombre = texto no vacío

telefono = 10 dígitos, permitiendo espacios y guiones en la captura

descuento = fracción entre 0 y 1

total = subtotal - descuento aplicado, redondeado a dos decimales

fecha_entrega = *fecha en formato AAAA-MM-DD*

## Uso de IA

Se usó Copilot como apoyo para convertir los almacenes y datos observables del sistema
de pedidos en una primera versión de entidades y definiciones del diccionario.
Se verificó que cada entidad corresponde a un almacén, que los identificadores son
únicos y estables, y que los flujos no copian datos innecesarios del sistema.
