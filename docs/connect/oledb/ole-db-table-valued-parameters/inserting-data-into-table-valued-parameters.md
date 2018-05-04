---
title: Insertar datos en parámetros con valores de tabla | Documentos de Microsoft
description: Usar el controlador OLE DB para SQL Server para insertar datos en parámetros con valores de tabla
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, inserting data into
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: e76dbb5bc5624b0295fdab8e9c36607c64058878
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="inserting-data-into-table-valued-parameters"></a>Insertar datos en parámetros con valores de tabla
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador OLE DB para SQL Server admite dos modelos para el consumidor especifique datos para filas de parámetros con valores de tabla: un modelo de inserción y un modelo de extracción. Un ejemplo que muestra el modelo de extracción está disponible; vea [ejemplos de programación de datos de SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
> [!NOTE]  
>  Una columna de parámetros con valores de tabla debe tener valores no predeterminados en todas las filas o valores predeterminados en todas las filas. No es posible tener valores predeterminados en algunas filas y en otras no. Por lo tanto, en enlaces de parámetros con valores de tabla, los únicos valores de estado permitidos en datos de columnas de conjunto de filas de parámetros con valores de tabla son DBSTATUS_S_ISNULL y DBSTATUS_S_OK. DBSTATUS_S_DEFAULT generará un error y el valor de estado enlazado se establecerá en DBSTATUS_E_BADSTATUS.  
  
## <a name="push-model-loads-all-table-valued-paremeter-data-in-memory"></a>Modelo de inserción (carga todos los datos de parámetros con valores de tabla en memoria)  
 El modelo de inserción es similar al uso de conjuntos de parámetros (es decir, el parámetro DBPARAMS en ICommand:: Execute). El modelo de inserción solo se usa si se usan objetos de conjunto de filas de parámetros con valores de tabla sin una implementación personalizada de interfaces IRowset. Se recomienda usar el modelo de inserción cuando el número de filas del conjunto de filas de parámetros con valores de tabla sea pequeño y no se espere que vaya a haber un exceso de presión de memoria en la aplicación. Este modelo es más sencillo que el modelo de extracción, ya que no requiere ninguna otra funcionalidad por parte de la aplicación del consumidor más que la actualmente común en aplicaciones OLE DB típicas.  
  
 Se espera que el consumidor proporcione todos los datos de parámetro con valores de tabla al proveedor antes de ejecutar un comando. Para proporcionar los datos, el consumidor rellena un objeto de conjunto de filas de parámetros con valores de tabla por cada parámetro con valores de tabla. El objeto de conjunto de filas de parámetro con valores de tabla expone las operaciones Insert, Set y Delete del conjunto de filas, que el consumidor usará para manipular los datos de parámetros con valores de tabla. El proveedor capturará los datos de este objeto de conjunto de filas de parámetros con valores de tabla en tiempo de ejecución.  
  
 Cuando se proporciona al consumidor un objeto de conjunto de filas de parámetros con valores de tabla, el consumidor puede procesarlo como un objeto de conjunto de filas. El consumidor puede obtener la información de tipo de cada columna (tipo, longitud máxima, precisión y escala) mediante el método de interfaz IColumnsInfo:: GetColumnInfo o IColumnsRowset:: GetColumnsRowset. A continuación, el consumidor crea un descriptor de acceso para especificar los enlaces de los datos. El paso siguiente consiste en insertar filas de datos en el conjunto de filas de parámetros con valores de tabla. Esto puede hacerse mediante el uso de IRowsetChange:: insertRow. IRowsetChange:: SetData o IRowsetChange:: DeleteRows también se utiliza en el objeto de conjunto de filas de parámetros con valores de tabla si tiene que manipular los datos. Los objetos de conjunto de filas de parámetros con valores de tabla son objetos en los que se cuentan las referencias, similares a los objetos de flujo.  
  
 Si se usa IColumnsRowset:: GetColumnsRowset, habrá posteriores llamadas a IRowset:: GetNextRows, IRowset:: GetData y IRowset::ReleaseRows métodos en el objeto de conjunto de filas de la columna resultante.  
  
 Después de que el controlador OLE DB para SQL Server empieza a ejecutar el comando, los valores de parámetro con valores de tabla se capturan de este objeto de conjunto de filas de parámetros con valores de tabla y se envían al servidor.  
  
 El modelo de inserción requiere un trabajo mínimo por parte del consumidor pero usa más memoria que el modelo de extracción, porque todos los datos de parámetro con valores de tabla deben estar en memoria en tiempo de ejecución.  
  
## <a name="pull-model-obtaining-table-valued-parameter-data-on-demand-from-the-consumer"></a>Modelo de extracción (obtener datos de parámetros con valores de tabla a petición del consumidor)  
 El modelo de extracción resulta útil en dos escenarios:  
  
-   Para transmitir filas por secuencias.  
  
-   Si se usa un conjunto de filas de otro proveedor como valor de parámetro con valores de tabla.  
  
 En el modelo de extracción, el consumidor proporciona datos a petición al proveedor. Use este enfoque si la aplicación tiene muchas inserciones de datos y los datos de conjunto de filas de parámetros con valores de tabla en memoria podrían dar lugar a un acceso excesivo a la memoria. Si se usan varios proveedores OLE DB, el modelo de extracción del consumidor permite que el consumidor proporcione cualquier objeto de conjunto de filas como valor de parámetro con valores de tabla.  
  
 Para usar el modelo de extracción, los consumidores deben proporcionar su propia implementación de un objeto de conjunto de filas. Cuando se usa el modelo de extracción con conjuntos de filas de parámetro con valores de tabla (CLSID_ROWSET_TVP), el consumidor se debe agregar el objeto de conjunto de filas de parámetro con valores de tabla que el proveedor expone a través de la ITableDefinitionWithConstraints:: Método CreateTableWithConstraints o el método IOpenRowset:: OpenRowset. Solo se espera que el objeto de consumidor invalide la implementación de la interfaz IRowset. Debe invalidar las funciones siguientes:  
  
-   IRowset:: GetNextRows  
  
-   IRowset::AddRefRows  
  
-   IRowset:: GetData  
  
-   IRowset::ReleaseRows  
  
-   IRowset:: RestartPosition  
  
 Controlador de OLE DB para SQL Server leerá una o más filas a la vez del consumidor de objeto de conjunto de filas para admitir el comportamiento de transmisión por secuencias en parámetros con valores de tabla. Por ejemplo, el usuario podría tener los datos del conjunto de filas de parámetro con valores de tabla en el disco (no en memoria) y puede implementar la funcionalidad para leer los datos desde el disco cuando sea necesario por el controlador OLE DB para SQL Server.  
  
 El consumidor comunicará su formato de datos al controlador de OLE DB para SQL Server utilizando IAccessor:: CreateAccessor en el objeto de conjunto de filas de parámetros con valores de tabla. Al leer los datos del búfer del consumidor, el proveedor comprueba que todas las columnas de escritura no predeterminadas están disponibles a través de al menos un identificador de descriptor de acceso, y usa los identificadores correspondientes para leer los datos de las columnas. Para evitar la ambigüedad, debería haber una correspondencia uno a uno entre una columna de conjunto de filas de parámetros con valores de tabla y un enlace. Los enlaces duplicados a la misma columna generarán un error. Además, cada descriptor de acceso debe tener la *iOrdinal* miembro de DBBindings en secuencia. Habrá tantas llamadas a IRowset:: GetData como el número de descriptores de acceso de cada fila y el orden de las llamadas se basará en el orden de *iOrdinal* valor de menor a mayor.  
  
 Se espera que el proveedor implemente la mayoría de las interfaces expuestas por el objeto de conjunto de filas de parámetros con valores de tabla. El consumidor implementará un objeto de conjunto de filas con interfaces mínimas (IRowset). Debido a la agregación oculta, el objeto de conjunto de filas de parámetros con valores de tabla implementará todas las demás interfaces obligatorias del objeto de conjunto de filas.  
  
 En cualquier otro objeto de conjunto de filas, como los objetos de conjunto de filas que se obtienen para cualquier proveedor OLE DB, el conjunto de filas proporcionado por el consumidor debe implementar todas las interfaces obligatorias del objeto de conjunto de filas, tal y como se indica en la especificación de OLE DB.  
  
 En el momento de ejecución, controlador de OLE DB para SQL Server volverá a llamar al objeto de conjunto de filas para capturar filas y leer los datos de columna.  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar con valores de tabla parámetros & #40; OLE DB & #41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
