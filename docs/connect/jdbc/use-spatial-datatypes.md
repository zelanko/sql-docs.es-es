---
title: Uso de los tipos de datos espaciales | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ce3df0755799e907bb286e10f5711a58a48135bb
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782471"
---
# <a name="using-spatial-datatypes"></a>Utilizar tipos de datos espaciales

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Se admiten los tipos de datos espaciales (geometría y geografía) a partir de versión de vista previa del controlador JDBC 6.5.0. Los tipos de datos espaciales no se admiten con procedimientos almacenados, los parámetros con valores de tabla (TVP), BulkCopy y Always Encrypted. Esta página muestra que varios casos de uso de tipos de datos Geometry y Geography con el controlador JDBC. Para obtener información general sobre los tipos de datos espaciales, consulte [información general de los tipos de datos espaciales](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview) página.

## <a name="creating-a-geometry--geography-object"></a>Creación de un objeto Geometry / objeto de geografía

Hay dos formas principales para crear una geometría / objeto de geografía - ser convertir desde un Well-Known Text (WKT) de o un Well-Known Binary (WKB).

### <a name="creating-from-wkt"></a>Crear a partir de WKT

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

Esto creará un objeto Geometry de LINESTRING con la identificador de sistema de referencia espacial (SRID) 0 y un objeto de geografía con SRID 4326.

### <a name="creating-from-wkb"></a>Crear a partir del WKB

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

Esto creará un objeto Geometry y Geography que es equivalente a los que se creó anteriormente desde el WKT.

## <a name="working-with-a-geometry--geography-object"></a>Trabajar con un objeto Geometry / objeto de geografía

Suponiendo que el usuario tiene una tabla en SQL Server como a continuación:

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Un script de ejemplo para insertar un valor de geometría sería:

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

Lo mismo se puede hacer el equivalente de geografía, mediante una columna de geografía y **setGeography()** método.

Para leer una geometría o columna de geografía:

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

Lo mismo se puede hacer el equivalente de geografía, mediante una columna de geografía y **getGeography()** método.

## <a name="newly-introduced-apis"></a>Recién introducidas API

Estas son las nuevas API públicas que se han introducido con esta versión, en las clases **SQLServerPreparedStatement**, **SQLServerResultSet**, **geometría**y  **Geography**.

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|Método|Descripción|
|:------|:----------|
|void setGeometry (int n, geometría x)| Establece el parámetro designado para el objeto de clase microsoft.sql.Geometry determinado.
|void setGeography (int n, Geography x)| Establece el parámetro designado para el objeto de clase microsoft.sql.Geography determinado.

### <a name="sqlserverresultset"></a>SQLServerResultSet

|Método|Descripción|
|:------|:----------|
|Geometría getGeometry (colunIndex int)| Devuelve el valor de la columna designada en la fila actual de este objeto de conjunto de resultados como un objeto com.microsoft.sqlserver.jdbc.Geometry en el lenguaje de programación Java.
|Geometría getGeometry (columnName cadena)| Devuelve el valor de la columna designada en la fila actual de este objeto de conjunto de resultados como un objeto com.microsoft.sqlserver.jdbc.Geometry en el lenguaje de programación Java.
|Geography getGeography (colunIndex int)| Devuelve el valor de la columna designada en la fila actual de este objeto de conjunto de resultados como un objeto com.microsoft.sqlserver.jdbc.Geography en el lenguaje de programación Java.
|Geography getGeography (columnName cadena)| Devuelve el valor de la columna designada en la fila actual de este objeto de conjunto de resultados como un objeto com.microsoft.sqlserver.jdbc.Geography en el lenguaje de programación Java.

### <a name="geometry"></a>Geometry

|Método|Descripción|
|:------|:----------|
|STGeomFromText (wkt String, int SRID) de geometría| Constructor para una instancia de Geometry a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
|Geometry STGeomFromWKB(byte[] wkb)| Constructor para una instancia de Geometry a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC).
|Geometrías deserializar (byte [] wkb)| Constructor para una instancia de geometría de un formato interno de SQL Server para los datos espaciales.
|Análisis de geometría (cadena wkt)| Constructor para una instancia de Geometry a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC). Identificador de referencia espacial valor predeterminado es 0.
|Punto de geometría (doble, x, doble y SRID int)| Constructor para una instancia de Geometry que representa una instancia Point de sus valores X e Y y un identificador de referencia espacial.
|Cadena STAsText()| Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de Geometry. Este texto no contendrá ningún valor Z (elevación) ni M (medida) perteneciente a la instancia.
|byte[] STAsBinary()| Devuelve la representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC) de una instancia de Geometry. Este valor no contendrá ningún valor Z o M perteneciente a la instancia.
|byte[] serialize()| Devuelve los bytes que representan un formato interno de SQL Server del tipo Geometry.
|booleano hasM()| Devuelve si el objeto contiene un valor M (medida).
|booleano hasZ()| Devuelve si el objeto contiene un valor Z (elevación).
|GetX() dobles| Devuelve el valor de la coordenada X.
|GetY() dobles| Devuelve el valor de coordenada Y.
|GetM() dobles| Devuelve el valor M (medida) del objeto.
|GetZ() dobles| Devuelve el valor Z (elevación) del objeto.
|int getSrid()| Devuelve el valor de identificador de referencia espacial (SRID).
|isNull() booleano| Devuelve si el objeto Geometry es null.
|int STNumPoints()| Devuelve el número de puntos en el objeto de geometría.
|String STGeometryType()| Devuelve el nombre del tipo de Open Geospatial Consortium (OGC) representado por una instancia de Geometry.
|String asTextZM()| Devuelve la representación Well-Known Text (WKT) del objeto Geometry.
|String toString()| Devuelve la representación de la cadena del objeto Geometry.

### <a name="geography"></a>Geografía

|Método|Descripción|
|:------|:----------|
|STGeomFromText (wkt String, int SRID) de geografía| Constructor para una instancia de Geography a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
|Geography STGeomFromWKB(byte[] wkb)| Constructor para una instancia de Geography a partir de una representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC).
|Geography deserialize(byte[] wkb)| Constructor para una instancia de Geography desde un formato interno de SQL Server para los datos espaciales.
|Análisis de geografía (cadena wkt)| Constructor para una instancia de Geography a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC). Identificador de referencia espacial valor predeterminado es 0.
|Punto de geografía (doble lon, LAT. doble, SRID int)| Constructor para una instancia de Geography que representa una instancia de Point a partir de su longitud y latitud y un identificador de referencia espacial.
|Cadena STAsText()| Devuelve la representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) de una instancia de Geography. Este texto no contendrá ningún valor Z (elevación) ni M (medida) perteneciente a la instancia.
|byte[] STAsBinary())| Devuelve la representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC) de una instancia de Geography. Este valor no contendrá ningún valor Z o M perteneciente a la instancia.
|byte[] serialize()| Devuelve los bytes que representan un formato interno de SQL Server del tipo Geography.
|booleano hasM()| Devuelve si el objeto contiene un valor M (medida).
|booleano hasZ()| Devuelve si el objeto contiene un valor Z (elevación).
|GetLatitude() dobles| Devuelve el valor de latitud.
|Double getLongitude()| Devuelve el valor de longitud.
|GetM() dobles| Devuelve el valor M (medida) del objeto.
|GetZ() dobles| Devuelve el valor Z (elevación) del objeto.
|int getSrid()| Devuelve el valor de identificador de referencia espacial (SRID).
|isNull() booleano| Devuelve si el objeto de geografía es null.
|int STNumPoints()| Devuelve el número de puntos en el objeto de geografía.
|String STGeographyType()| Devuelve el nombre del tipo de Open Geospatial Consortium (OGC) representado por una instancia de Geography.
|String asTextZM()| Devuelve la representación Well-Known Text (WKT) del objeto Geography.
|String toString()| Devuelve la representación de la cadena del objeto Geography.

## <a name="limitations-of-spatial-datatypes"></a>Limitaciones de los tipos de datos espaciales

1. El sub-tipos de datos espaciales **CircularString**, **CompoundCurve**, **CurvePolygon**, y **FullGlobe** solo se admite a partir de desde SQL Server 2012 y versiones posteriores.

2. Always Encrypted no se puede usar con tipos de datos espaciales.

3. Procedimientos almacenados, TVP y BulkCopy actualmente no se admiten operaciones con tipos de datos espaciales.

## <a name="see-also"></a>Consulte también

[Ejemplo de tipos de datos espaciales (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
