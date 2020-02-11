---
title: MERGE en paquetes de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- MERGE statement [SQL Server]
ms.assetid: 7e44a5c2-e6d6-4fe2-a079-4f95ccdb147b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47940abbbbf4ebf41c85bb0c8a7ee6f986a570bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62831887"
---
# <a name="merge-in-integration-services-packages"></a>MERGE en paquetes de Integration Services
  En la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], la instrucción SQL de una tarea Ejecutar SQL puede contener una instrucción MERGE. Esta instrucción MERGE permite llevar a cabo varias operaciones INSERT, UPDATE y DELETE en una única instrucción.  
  
 Para utilizar la instrucción MERGE en un paquete, siga estos pasos:  
  
-   Cree una tarea Flujo de datos que cargue, transforme y guarde los datos de origen en una tabla temporal o de ensayo.  
  
-   Cree una tarea Ejecutar SQL que incluya la instrucción MERGE.  
  
-   Conecte la tarea Flujo de datos a la tarea Ejecutar SQL, y use los datos de la tabla de ensayo como entrada para la instrucción MERGE.  
  
    > [!NOTE]  
    >  Aunque una instrucción MERGE normalmente requiere una tabla de ensayo en este escenario, generalmente ofrece un mayor rendimiento que el de la búsqueda fila por fila realizada por la transformación Búsqueda. La instrucción MERGE también resulta útil cuando el gran tamaño de una tabla de búsqueda pondría a prueba la memoria que la transformación de búsquedas puede usar para almacenar en caché su tabla de referencia.  
  
 El resto de este tema explica algunos usos adicionales de la instrucción MERGE.  
  
 Para obtener un componente de destino de ejemplo que admite el uso de la instrucción MERGE, vea el ejemplo de la comunidad de CodePlex, [MERGE Destination](https://go.microsoft.com/fwlink/?LinkId=141215).  
  
## <a name="using-merge"></a>Usar MERGE  
 Normalmente, la instrucción MERGE se usa cuando se desea aplicar ciertos cambios, como inserciones, actualizaciones y eliminaciones, de una tabla a otra. En las versiones anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], este proceso requería una transformación Búsqueda y varias transformaciones Comando de OLE DB. La transformación Búsqueda realizaba una búsqueda fila por fila para determinar si la fila era nueva o se había modificado. A continuación, las transformaciones Comando de OLE DB llevaban a cabo las operaciones INSERT, UPDATE y DELETE necesarias. A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], una única instrucción MERGE puede reemplazar la transformación Búsqueda y las transformaciones Comando de OLE DB correspondientes.  
  
### <a name="merge-with-incremental-loads"></a>MERGE con cargas incrementales  
 La nueva función de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de captura de datos modificados facilita la realización confiable de cargas incrementales durante el almacenamiento de datos. Como alternativa al uso de transformaciones Comando de OLE DB con parámetros para realizar inserciones y actualizaciones, se puede usar la instrucción MERGE para combinar ambas operaciones.  
  
 Para más información, vea [Aplicar los cambios al destino](../change-data-capture/apply-the-changes-to-the-destination.md).  
  
#### <a name="merge-in-other-scenarios"></a>MERGE en otros escenarios  
 En los escenarios siguientes, se puede utilizar la instrucción MERGE fuera o dentro de un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Sin embargo, a menudo se requiere un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para cargar estos datos desde varios orígenes heterogéneos, así como para combinarlos y limpiarlos posteriormente. Por lo tanto, puede ser interesante usar la instrucción MERGE en un paquete por su comodidad y su facilidad de mantenimiento.  
  
##### <a name="track-buying-habits"></a>Realizar un seguimiento de los hábitos de compra  
 La tabla FactBuyingHabits del almacenamiento de datos realiza un seguimiento de la última fecha en la que un cliente adquirió un determinado producto. Dicha tabla consta de las columnas ProductID, CustomerID y PurchaseDate. Todas las semanas, la base de datos transaccional genera una tabla PurchaseRecords que incluye las compras realizadas durante la semana. El objetivo es usar una única instrucción MERGE para combinar la información de la tabla PurchaseRecords con la de la tabla FactBuyingHabits. Para los pares de producto-cliente que no existen, la instrucción MERGE inserta nuevas filas. Para los pares de producto-cliente existentes, la instrucción MERGE actualiza la fecha de compra más reciente.  
  
###### <a name="track-price-history"></a>Realizar un seguimiento del historial de precios  
 La tabla DimBook representa la lista de libros en el inventario de un vendedor de libros e identifica el historial de precios de cada libro. Esta tabla tiene las siguientes columnas: ISBN, ProductID, Price, Shelf e IsCurrent. También incluye una fila para cada precio que ha tenido el libro. Una de estas filas contiene el precio actual. Para indicar la fila que contiene el precio actual, el valor de la columna IsCurrent para dicha fila se establece en 1.  
  
 Todas las semanas, la base de datos genera una tabla denominada WeeklyChanges que contiene los cambios de precio para la semana y los libros que se han agregado durante la misma. Una única instrucción MERGE permitirá aplicar los cambios de la tabla WeeklyChanges a la tabla DimBook. Esta instrucción MERGE inserta nuevas filas para las nuevas adquisiciones de libros, y actualiza la columna IsCurrent a 0 en las filas de libros existentes cuyos precios han cambiado. Dicha instrucción también inserta nuevas filas para los libros cuyos precios han cambiado, y establece el valor de la columna IsCurrent en 1 para estas filas.  
  
### <a name="merge-a-table-with-new-data-against-the-old-table"></a>Combinar una tabla que tiene nuevos datos con la tabla antigua  
 La base de datos modela las propiedades de un objeto mediante un “esquema abierto” (es decir, una tabla que contiene pares de nombre-valor para cada propiedad). La tabla Properties tiene tres columnas: EntityID, PropertyID y Value. La tabla NewProperties, que es una versión más reciente de dicha tabla, se debe sincronizar con la tabla Properties. Para sincronizar ambas tablas, puede utilizar una única instrucción MERGE que realice las operaciones siguientes:  
  
-   Eliminar las propiedades de la tabla Properties que no aparezcan en la tabla NewProperties.  
  
-   Actualizar los valores de las propiedades que aparecen en la tabla Properties con los nuevos valores incluidos en la tabla NewProperties.  
  
-   Insertar nuevas propiedades para las propiedades existentes en la tabla NewProperties pero que no aparecen en la tabla Properties.  
  
 Este enfoque es útil en escenarios similares a los escenarios de replicación, en los que el objetivo es mantener sincronizados los datos de dos tablas ubicadas en dos servidores.  
  
### <a name="track-inventory"></a>Realizar un seguimiento del inventario  
 La base de datos Inventory incluye una tabla ProductsInventory con las columnas ProductID y StockOnHand. La tabla Shipments, que contiene las columnas ProductID, CustomerID y Quantity, realiza un seguimiento de los envíos de los productos a los clientes. La tabla ProductInventory debe actualizarse diariamente basándose en la información de la tabla Shipments. Una única instrucción MERGE puede reducir el inventario en la tabla ProductInventory sobre la base de los envíos realizados. Si el inventario de un producto se ha reducido a 0, dicha instrucción MERGE también puede eliminar la fila del producto de la tabla ProductInventory.  
  
  
