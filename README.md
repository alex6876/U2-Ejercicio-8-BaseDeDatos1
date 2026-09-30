# Ejercicio — Base de Datos de Gestión de Inventario, Depósitos y Órdenes de Compra



Proyecto enfocado en la modelación Entidad-Relación (DER / MER) e implementación de base de datos relacional para la gestión integral de inventario, almacenamiento en depósitos, proveedores y órdenes de compra de mercadería.

---

## Descripción

El sistema modela una estructura de datos relacional para el control logístico y abastecimiento de productos en una organización. Permite administrar el catálogo global de productos y la distribución física de sus existencias en múltiples depósitos o almacenes, gestionar los proveedores asociados con sus condiciones comerciales y precios de costo, así como coordinar la emisión de órdenes de compra con el desglose del detalle de ítems solicitados y la asignación del depósito de destino.

---

## Funcionalidades e Implementación

### Entidades y Atributos

* Producto:


* id_codigo de barra: Clave primaria identificadora única del producto.


* descripción: Detalle comercial o especificación del producto.


* peso: Peso físico de la unidad.


* dimensiones: Medidas físicas o volumen del paquete/producto.


* Stock: Cantidad global disponible en inventario.




* Deposito:


* id_Deposito: Clave primaria identificadora del almacén o depósito.


* nombre: Nombre o denominación de la sucursal/almacén.


* dirección: Ubicación geográfica o domicilio físico del depósito.


* cargo responsable: Nombre o puesto de la persona encargada del depósito.


* telefono: Teléfono de contacto directo del almacén.




* Stock:


* id_codigo de barra: Clave foránea que referencia al producto almacenado.


* id_Deposito: Clave foránea que referencia al depósito físico donde reside la existencia.


* cantidad stock: Unidades físicas guardadas en dicha localización específica.


* ubicación: Ubicación exacta dentro del depósito (ej. estante, pasillo, módulo).


* fecha actualización: Última fecha de registro de movimiento de existencias.




* Proveedor:


* id_CUIL: Clave primaria única de identificación tributaria o CUIT/CUIL del proveedor.


* razón social: Nombre legal o razón social de la empresa proveedora.


* persona de contacto: Nombre del representante o contacto comercial.


* país de origen: País de procedencia o residencia del proveedor.


* Correo electrónico: Email de contacto o facturación.




* Producto-Proveedor:


* id_codigo de barra: Clave foránea que referencia al producto ofrecido.


* id_CUIL: Clave foránea que referencia al proveedor adjudicado.


* precio costo: Precio pactado o costo unitario del proveedor para dicho producto.


* cantidad de stock: Volumen de stock disponible según el proveedor.


* condicion de pago: Términos de pago o financiamiento establecidos (ej. 30 días, contado).




* Orden de Compra:


* id_nroOrden: Clave primaria única de la orden de compra emitida.


* fecha de emisión: Fecha en que se genera la orden.


* estado: Estado del pedido (ej. pendiente, autorizada, recibida, cancelada).


* deposito de destino: Dirección o especificación de recepción del pedido.


* id_Deposito: Clave foránea al depósito donde ingresará la mercadería.




* Detalle-Orden-Compra:


* id_nroOrden: Clave foránea que vincula el ítem a la orden de compra correspondiente.


* id_codigo de barra: Clave foránea del producto solicitado.


* cantidad pedida: Número de unidades requeridas.


* precioPactado: Precio fijado por unidad para esa compra.


* subtotal: Importe total resultante para ese renglón de compra.





---

## Relaciones del Modelo

1. Producto ↔ Stock (Relación 1:N / N:1):


* Un producto puede tener existencias distribuidas en múltiples almacenes o depósitos.




2. Deposito ↔ Stock (Relación 1:N / N:1):


* Un depósito alberga múltiples registros de stock pertenecientes a distintos productos de catálogo.




3. Producto ↔ Proveedor (Relación N:M via Producto-Proveedor):


* Un producto puede ser provisto por diferentes proveedores y cada proveedor puede suministrar una variedad de productos. La relación se modela mediante la entidad intermedia `Producto-Proveedor` que almacena precios y condiciones comerciales.




4. Proveedor ↔ Producto-Proveedor (Relación 1:N / N:1):


* Un proveedor registra sus ofertas de productos en la tabla intermedia.




5. Proveedor / Producto-Proveedor ↔ Orden de Compra (Relación N:1):


* Una orden de compra se emite hacia un proveedor específico definiendo las condiciones de abastecimiento.




6. Deposito ↔ Orden de Compra (Relación 1:N):


* Un depósito recepta múltiples órdenes de compra destinadas a reponer sus inventarios.




7. Orden de Compra ↔ Detalle-Orden-Compra (Relación 1:N):


* Una orden de compra incluye uno o más ítems/renglones detallados de adquisición.




8. Producto ↔ Detalle-Orden-Compra (Relación N:1):


* Un mismo producto de catálogo puede aparecer en múltiples detalles de órdenes de compra emitidas.
* 
