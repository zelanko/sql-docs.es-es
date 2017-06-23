---
title: Dar formato JSON a los resultados de consulta con FOR JSON (SQL Server) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 06095384c6f6ec876e0d103186b1269d19056987
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>Dar formato JSON a los resultados de consulta con FOR JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Dé formato JSON a los resultados de las consultas o exporte datos de SQL Server como JSON mediante la adición de la cláusula **FOR JSON** a una instrucción **SELECT**. Use la **FOR JSON** cláusula para simplificar las aplicaciones cliente delegando el formato de salida JSON desde las aplicaciones cliente para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
 Cuando se usa la cláusula **FOR JSON** , puede especificar la estructura de la salida de forma explícita o dejar que la estructura de la instrucción SELECT determine la salida.  
  
-   Use **FOR JSON PATH** para mantener el control total sobre el formato de la salida JSON. Puede crear objetos contenedores y anidar propiedades complejas.  
  
-   Use **FOR JSON AUTO** dar formato JSON a la salida automáticamente en función de la estructura de la instrucción SELECT.  
  
Este es un ejemplo de una instrucción **SELECT** con la cláusula **FOR JSON** y su salida.
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png "FOR JSON")  
  
## <a name="maintain-control-over-json-output-with-for-json-path"></a>Mantener el control sobre la salida JSON con FOR JSON PATH
En el modo **PATH** , puede usar la sintaxis de puntos (por ejemplo, `'Item.Price'` ) para dar formato a la salida anidada.  

Esta es una consulta de ejemplo en la que se usa el modo **PATH** con la cláusula **FOR JSON** . En el ejemplo siguiente también se usa la opción **ROOT** para especificar un elemento raíz con nombre. 
  
 ![Diagrama de flujo de salida FOR JSON](../../relational-databases/json/media/forjson-example1.png "Diagrama de flujo de salida FOR JSON")  

### <a name="more-info"></a>Más información
Para obtener más información y ejemplos, vea [formato de salida JSON anidada con el modo PATH &#40; SQL Server &#41; ](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).

Para ver la sintaxis y el uso, consulte [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  

## <a name="let-the-select-statement-control-json-output-with-for-json-auto"></a>Permitir que el control de la instrucción SELECT del resultado JSON con FOR JSON AUTO
En el modo **AUTO** , la estructura de la instrucción SELECT determina el formato de la salida JSON. Los valores **null** no se incluyen en la salida de forma predeterminada. Puede usar la opción **INCLUDE_NULL_VALUES** para cambiar este comportamiento.  

Esta es una consulta de ejemplo en la que se usa el modo **AUTO** con la cláusula **FOR JSON** .
 
**Consulta:**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO  
```  
  
 **Resultado**  
  
```json  
[{
    "name": "John"
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
### <a name="more-info"></a>Más información
Para obtener más información y ejemplos, vea [formato de salida JSON automáticamente con el modo AUTO &#40; SQL Server &#41; ](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).

Para ver la sintaxis y el uso, consulte [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="control-other-json-output-options"></a>Controlar otras opciones de salida JSON  
Controlar la salida de la **FOR JSON** cláusula mediante el uso de las siguientes opciones adicionales.  
  
-   **RAÍZ**. Para agregar un solo elemento de nivel superior a la salida JSON, especifique la opción **ROOT** . Si no especifica esta opción, la salida JSON no tiene un elemento raíz. Para obtener más información, vea [Agregar un nodo raíz a la salida JSON con la opción ROOT &#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
-   **INCLUDE_NULL_VALUES**. Para incluir valores NULL en la salida JSON, especifique la opción **INCLUDE_NULL_VALUES** . Si no especifica esta opción, la salida no incluye las propiedades JSON para los valores NULL en los resultados de la consulta. Para obtener más información, consulte [incluir valores Null en la salida de JSON con la opción INCLUDE_NULL_VALUES &#40; SQL Server &#41; ](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).   

-   **WITHOUT_ARRAY_WRAPPER**. Para quitar los corchetes que rodean la salida JSON de la cláusula **FOR JSON** de manera predeterminada, especifique la opción **WITHOUT_ARRAY_WRAPPER** . Utilice esta opción para generar un objeto JSON único como salida de un sola fila de resultados. Si no especifica esta opción, la salida JSON es un formato como una matriz, es decir, está delimitado por corchetes. Para obtener más información, vea [Quitar corchetes de la salida JSON con la opción WITHOUT_ARRAY_WRAPPER &#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md). 
   
## <a name="output-of-the-for-json-clause"></a>Salida de la cláusula FOR JSON  
 La salida de la cláusula **FOR JSON** tiene las siguientes características.  
  
1.  El conjunto de resultados contiene una sola columna.
    -   Un conjunto de resultados pequeño puede contener una sola fila.
    -   Un conjunto de resultados grande divide la cadena JSON larga en varias filas.
        -   De forma predeterminada, SQL Server Management Studio (SSMS) concatena los resultados en una sola fila cuando el valor de salida es **resultados a cuadrícula**. La barra de estado SSMS muestra el recuento de filas real.
        -   Otras aplicaciones cliente pueden requerir código para concatenar los resultados extensa combinando el contenido de varias filas. Para obtener un ejemplo de este código en una aplicación de C#, vea [salida Use FOR JSON en una aplicación de cliente de C#](https://docs.microsoft.com/en-us/sql/relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server#use-for-json-output-in-a-c-client-app).
  
     ![Ejemplo de salida FOR JSON](../../relational-databases/json/media/forjson-example2.png "Ejemplo de salida FOR JSON")  
  
2.  Se da formato a los resultados como una matriz de objetos JSON.  
  
    -   El número de elementos de la matriz JSON es igual al número de filas en los resultados de la instrucción SELECT (antes de que se aplica la cláusula FOR JSON). 
  
    -   Cada fila de los resultados de la instrucción SELECT (antes de que se aplica la cláusula FOR JSON) se convierte en un objeto JSON independiente en la matriz.  
  
    -   Cada columna de los resultados de la instrucción SELECT (antes de la cláusula se aplica consulta JSON FOR) se convierte en una propiedad del objeto JSON.  
  
3.  Tanto los nombres de las columnas como sus valores van acompañados de un carácter de escape, como reza la sintaxis de JSON. Para obtener más información, vea [Cómo FOR JSON inserta caracteres de escape en los caracteres especiales y caracteres de control &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md).
  
### <a name="example"></a>Ejemplo
Este es un ejemplo que muestra cómo el **FOR JSON** cláusula da formato al resultado JSON.  
  
**Resultados de la consulta**  
  
|||||  
|-|-|-|-|  
|**A**|**B**|**C**|**D**|  
|10|11|12|X|  
|20|21|22|S|  
|30|31|32|Z|  
  
 **Salida JSON**  
  
```json  
[{
    "A": 10,
    "B": 11,
    "C": 12,
    "D": "X"
}, {
    "A": 20,
    "B": 21,
    "C": 22,
    "D": "Y"
}, {
    "A": 30,
    "B": 31,
    "C": 32,
    "D": "Z"
}] 
```  
 Para más información sobre lo que ve en la salida de la cláusula **FOR JSON**, vea los temas siguientes.  
-   [Conversión por parte de FOR JSON de tipos de datos de SQL Server en tipos de datos JSON &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server.md)  
La cláusula **FOR JSON** usa las reglas descritas en este tema para convertir tipos de datos SQL a tipos JSON en la salida JSON.  

-   [Cómo FOR JSON inserta caracteres de escape en los caracteres especiales y caracteres de control &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)  
 La cláusula **FOR JSON** inserta un carácter de escape en los caracteres especiales y representa caracteres de control en la salida JSON, como se describe en este tema.  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [Uso de salidas FOR JSON en SQL Server y en aplicaciones cliente &#40;SQL Server&#41;](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  

