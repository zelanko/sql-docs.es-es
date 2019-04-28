---
title: Manipular datos UDT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- data deletions [CLR integration]
- data insertions [CLR integration]
- CONVERT function
- data updates [CLR integration]
- comparing data
- updating data [CLR integration]
- removing data
- IsByteOrdered property
- variables [CLR integration]
- data manipulation [CLR integration]
- user-defined types [CLR integration], data manipulation
- deleting data
- UDTs [CLR integration], data manipulation
- invoking UDT methods
- inserting data
ms.assetid: 51b1a5f2-7591-4e11-bfe2-d88e0836403f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 11aa57037a1ea92bd72ed2eaa581d34baff8a122
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874311"
---
# <a name="manipulating-udt-data"></a>Manipular datos UDT
  [!INCLUDE[tsql](../../includes/tsql-md.md)] no proporciona ninguna sintaxis especializada para las instrucciones INSERT, UPDATE o DELETE al modificar datos en columnas de tipo definido por el usuario (UDT). Para convertir los tipos de datos nativos al tipo UDT, se utilizan las funciones CAST o CONVERT de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="inserting-data-in-a-udt-column"></a>Insertar datos en una columna UDT  
 La siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones insertan tres filas de datos de ejemplo en el **puntos** tabla. El **punto** X formado por tipo de datos de valores enteros e Y que se exponen como propiedades del UDT. Se deben usar funciones CAST o CONVERT para convertir la coma valores X e Y para el **punto** tipo. Las dos primeras instrucciones use la función CONVERT para convertir un valor de cadena para la **punto** tipo y la tercera instrucción utiliza la función CAST:  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
## <a name="selecting-data"></a>Seleccionar datos  
 La siguiente instrucción SELECT selecciona el valor binario del UDT.  
  
```  
SELECT ID, PointValue FROM dbo.Points  
```  
  
 Para ver la salida mostrada en un formato legible, llame a la `ToString` método de la **punto** UDT, que convierte el valor en su representación de cadena.  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points;  
```  
  
 Esto produce el siguiente resultado.  
  
```  
IDPointValue  
----------  
13,4  
21,5  
31,99  
```  
  
 También puede utilizar las funciones CAST y CONVERT de [!INCLUDE[tsql](../../includes/tsql-md.md)] para lograr los mismos resultados.  
  
```  
SELECT ID, CAST(PointValue AS varchar)   
FROM dbo.Points;  
  
SELECT ID, CONVERT(varchar, PointValue)   
FROM dbo.Points;  
```  
  
 El **punto** UDT expone sus coordenadas X e Y como propiedades, que, a continuación, puede seleccionar individualmente. La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] selecciona las coordenadas X e Y por separado:  
  
```  
SELECT ID, PointValue.X AS xVal, PointValue.Y AS yVal   
FROM dbo.Points;  
```  
  
 Las propiedades X e Y devuelven un valor entero, que se muestra en el conjunto de resultados.  
  
```  
IDxValyVal  
----------  
134  
215  
3199  
```  
  
## <a name="working-with-variables"></a>Trabajar con variables  
 Puede trabajar con variables si utiliza la instrucción DECLARE para asignar una variable a un tipo UDT. Las instrucciones siguientes asignan un valor mediante la instrucción SET de [!INCLUDE[tsql](../../includes/tsql-md.md)] y muestran los resultados con una llamada al método `ToString` del UDT en la variable:  
  
```  
DECLARE @PointValue Point;  
SET @PointValue = (SELECT PointValue FROM dbo.Points  
    WHERE ID = 2);  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 El conjunto de resultados muestra el valor variable:  
  
```  
PointValue  
----------  
-1,5  
```  
  
 Las siguientes instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] logran el mismo resultado utilizando SELECT en lugar de SET para la asignación de variable:  
  
```  
DECLARE @PointValue Point;  
SELECT @PointValue = PointValue FROM dbo.Points  
    WHERE ID = 2;  
SELECT @PointValue.ToString() AS PointValue;  
```  
  
 La diferencia entre el uso de SELECT y SET para la asignación de variable es que SELECT permite asignar varias variables en una instrucción SELECT, mientras que la sintaxis de SET exige que cada asignación de variable tenga su propia instrucción SET.  
  
## <a name="comparing-data"></a>Comparar datos  
 Puede utilizar operadores de comparación para comparar valores del UDT si ha establecido la propiedad `IsByteOrdered` en `true` al definir la clase. Para obtener más información, consulte [creación de un tipo definido por el usuario](creating-user-defined-types.md).  
  
```  
SELECT ID, PointValue.ToString() AS Points   
FROM dbo.Points  
WHERE PointValue > CONVERT(Point, '2,2');  
```  
  
 Puede comparar valores internos del UDT sin tener en cuenta el valor `IsByteOrdered` si los propios valores son comparables. La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] selecciona filas donde X es mayor que Y:  
  
```  
SELECT ID, PointValue.ToString() AS PointValue   
FROM dbo.Points  
WHERE PointValue.X < PointValue.Y;  
```  
  
 También puede utilizar operadores de comparación con variables, tal como se muestra en esta consulta que busca un PointValue correspondiente.  
  
```  
DECLARE @ComparePoint Point;  
SET @ComparePoint = CONVERT(Point, '3,4');  
SELECT ID, PointValue.ToString() AS MatchingPoint   
FROM dbo.Points  
WHERE PointValue = @ComparePoint;  
```  
  
## <a name="invoking-udt-methods"></a>Invocar métodos del UDT  
 También puede invocar métodos que se definen en el UDT en [!INCLUDE[tsql](../../includes/tsql-md.md)]. El **punto** clase contiene tres métodos `Distance`, `DistanceFrom`, y `DistanceFromXY`. Para las listas de código que se definen estos tres métodos, consulte [codificación de tipos](creating-user-defined-types-coding.md).  
  
 La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] llama al método `PointValue.Distance`:  
  
```  
SELECT ID, PointValue.X AS [Point.X],   
    PointValue.Y AS [Point.Y],  
    PointValue.Distance() AS DistanceFromZero   
FROM dbo.Points;  
```  
  
 Los resultados se muestran en la `Distance` columna:  
  
```  
IDXYDistance  
------------------------  
1345  
2155.09901951359278  
319999.0050503762308  
```  
  
 El `DistanceFrom` método toma un argumento de **punto** tipo de datos y muestra la distancia desde el punto especificado hasta PointValue:  
  
```  
SELECT ID, PointValue.ToString() AS Pnt,  
   PointValue.DistanceFrom(CONVERT(Point, '1,99')) AS DistanceFromPoint  
FROM dbo.Points;  
```  
  
 La salida muestra los resultados del método `DistanceFrom` en cada fila de la tabla:  
  
```  
ID PntDistanceFromPoint  
---------------------  
13,495.0210502993942  
21,594  
31,990  
```  
  
 El método `DistanceFromXY` toma los puntos de forma individual como argumentos:  
  
```  
SELECT ID, PointValue.X as X, PointValue.Y as Y,   
PointValue.DistanceFromXY(1, 99) AS DistanceFromXY   
FROM dbo.Points  
```  
  
 El conjunto de resultados es el mismo que en el método `DistanceFrom`.  
  
## <a name="updating-data-in-a-udt-column"></a>Actualizar datos en una columna UDT  
 Para actualizar datos en una columna UDT, utilice la instrucción UPDATE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. También puede utilizar un método del UDT para actualizar el estado del objeto. La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] actualiza una única fila en la tabla:  
  
```  
UPDATE dbo.Points  
SET PointValue = CAST('1,88' AS Point)  
WHERE ID = 3  
```  
  
 También puede actualizar los elementos UDT por separado. La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] solo actualiza la coordenada Y:  
  
```  
UPDATE dbo.Points  
SET PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Si el UDT se ha definido con el orden de bytes establecido en `true`, [!INCLUDE[tsql](../../includes/tsql-md.md)] puede evaluar la columna UDT en una cláusula WHERE.  
  
```  
UPDATE dbo.Points  
SET PointValue = '4,5'  
WHERE PointValue = '3,4';  
```  
  
### <a name="updating-limitations"></a>Limitaciones de la actualización  
 No puede actualizar varias propiedades a la vez mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]. Por ejemplo, la siguiente instrucción UPDATE genera un error porque no puede utilizar dos veces el mismo nombre de columna en una instrucción UPDATE.  
  
```  
UPDATE dbo.Points  
SET PointValue.X = 5, PointValue.Y = 99  
WHERE ID = 3  
```  
  
 Para actualizar individualmente cada punto, debe crear un método mutador en el ensamblado UDT de Point. A continuación, puede invocar el método mutador para actualizar el objeto en una instrucción UPDATE de [!INCLUDE[tsql](../../includes/tsql-md.md)], como en el siguiente ejemplo:  
  
```  
UPDATE dbo.Points  
SET PointValue.SetXY(5, 99)  
WHERE ID = 3  
```  
  
## <a name="deleting-data-in-a-udt-column"></a>Eliminar datos en una columna UDT  
 Para eliminar datos en un UDT, utilice la instrucción DELETE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. La siguiente instrucción elimina todas las filas de la tabla que coinciden con los criterios especificadas en la cláusula WHERE. Si omite la cláusula WHERE de una instrucción DELETE, se eliminarán todas las filas de la tabla.  
  
```  
DELETE FROM dbo.Points  
WHERE PointValue = CAST('1,99' AS Point)  
```  
  
 Utilice la instrucción UPDATE si desea quitar los valores de una columna UDT y conservar los valores de otra fila intactos. En este ejemplo se establece PointValue en NULL.  
  
```  
UPDATE dbo.Points  
SET PointValue = null  
WHERE ID = 2  
```  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con tipos definidos por el usuario en SQL Server](working-with-user-defined-types-in-sql-server.md)  
  
  
