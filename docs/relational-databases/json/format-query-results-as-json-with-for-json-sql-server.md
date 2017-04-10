---
title: "Dar formato JSON a los resultados de consulta con FOR JSON (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR JSON"
  - "JSON, exportar"
  - "exportar JSON"
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Dar formato JSON a los resultados de consulta con FOR JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Exporte datos de SQL Server como JSON o dé formato JSON a los resultados de las consultas mediante la adición de la cláusula **FOR JSON** a una instrucción **SELECT** .  
  
 Cuando se usa la cláusula **FOR JSON** , puede especificar la estructura de la salida de forma explícita o dejar que la estructura de la instrucción SELECT determine la salida.  
  
-   **Usar el modo PATH con la cláusula FOR JSON**. Si usa el modo **PATH** con la cláusula **FOR JSON** , tendrá un control total sobre el formato de la salida JSON. Puede crear objetos contenedores y anidar propiedades complejas.  
  
-   **Usar el modo AUTO con la cláusula FOR JSON**. Si usa el modo **AUTO** con la cláusula **FOR JSON** , se aplicará formato automáticamente a la salida JSON en función de la estructura de la instrucción SELECT.  
  
 Use la cláusula **FOR JSON** para delegar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la aplicación de formato a los resultados de JSON procedentes de aplicaciones cliente. Para obtener más información, vea [Uso de salidas FOR JSON en SQL Server y en aplicaciones cliente &#40;SQL Server&#41;](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md).  
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png "FOR JSON")  
  
## Usar el modo PATH con la cláusula FOR JSON  
 En este ejemplo se usa el modo **PATH** con la cláusula **FOR JSON** .

En el modo **PATH**, puede usar la sintaxis de puntos (por ejemplo, `'Item.Price'`) para dar formato a la salida anidada. En este ejemplo también se usa la opción **ROOT** para especificar un elemento raíz con nombre.  
-   Para obtener más información y ejemplos, vea [Formato de salida JSON anidada con el modo PATH &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).
-   Para ver la sintaxis y el uso, consulte [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md).  
  
 ![Diagram of flow of FOR JSON output](../../relational-databases/json/media/forjson-example1.png "Diagram of flow of FOR JSON output")  
  
## Usar el modo AUTO con la cláusula FOR JSON  
 Esta es una consulta de ejemplo en la que se usa el modo **AUTO** con la cláusula **FOR JSON** .

En el modo **AUTO** , la estructura de la instrucción SELECT determina el formato de la salida JSON. Los valores **null** no se incluyen en la salida de forma predeterminada. Puede usar la opción **INCLUDE_NULL_VALUES** para cambiar este comportamiento.  
  
-   Para obtener más información y ejemplos, vea [Aplicar formato a la salida JSON automáticamente con el modo AUTO &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).
-   Para ver la sintaxis y el uso, consulte [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md).  
  
 **Consulta:**  
  
```tsql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO  
```  
  
 **Resultado**  
  
```json  
[   
   { "name": "John" },  
   { "name": "Jane", "surname": "Doe" }  
]  
  
```  
  
## Controlar la salida JSON con opciones con la cláusula FOR JSON  
 Use las siguientes opciones para controlar la salida de la cláusula **FOR JSON** .  
  
 [Agregar un nodo raíz a la salida JSON con la opción ROOT &#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md)  
 Para agregar un solo elemento de nivel superior a la salida JSON, especifique la opción **ROOT**. Si no especifica la opción **ROOT** , la salida JSON no tiene un elemento raíz.  
  
 [Inclusión de valores NULL en la salida JSON con la opción INCLUDE_NULL_VALUES &#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md)  
 Para incluir valores NULL en la salida JSON, especifique la opción **INCLUDE_NULL_VALUES**. Si no especifica esta opción, la salida no incluye las propiedades JSON de los valores NULL en los resultados de la consulta.  
  
 [Quitar corchetes de la salida JSON con la opción WITHOUT_ARRAY_WRAPPER &#40;SQL Server&#41;](../../relational-databases/json/remove square brackets from json - without_array_wrapper option.md)  
 Para quitar los corchetes que rodean la salida JSON de la cláusula **FOR JSON** de manera predeterminada, especifique la opción **WITHOUT_ARRAY_WRAPPER**. Use esta opción para generar un objeto JSON único como salida. Si no especifica esta opción, la salida JSON aparecerá entre corchetes.  
  
 Para obtener más información sobre lo que ve en la salida de la cláusula **FOR JSON** , consulte los temas siguientes de esta sección.  
  
 [Conversión por parte de FOR JSON de tipos de datos de SQL Server en tipos de datos JSON &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server.md)  
 La cláusula **FOR JSON** usa las reglas descritas en este tema para convertir tipos de datos SQL a tipos JSON en la salida JSON.  
  
 [Cómo FOR JSON inserta caracteres de escape en los caracteres especiales y caracteres de control &#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)  
 La cláusula **FOR JSON** inserta un carácter de escape en los caracteres especiales y representa caracteres de control en la salida JSON, como se describe en este tema.  
  
## Salida de la cláusula FOR JSON  
 La salida de la cláusula **FOR JSON** tiene las siguientes características.  
  
1.  El conjunto de resultados contiene una sola columna. Un conjunto de resultados pequeño puede contener una sola fila. Un conjunto de resultados grande contiene varias filas.  
  
     ![Example of FOR JSON output](../../relational-databases/json/media/forjson-example2.png "Example of FOR JSON output")  
  
2.  Se da formato a los resultados como una matriz de objetos JSON.  
  
    -   El número de elementos de la matriz es igual al número de filas de los resultados.  
  
    -   Cada fila del conjunto de resultados se convierte en un objeto JSON independiente en la matriz.  
  
    -   Cada columna del conjunto de resultados se convierte en una propiedad del objeto JSON.  
  
3.  Tanto los nombres de las columnas como sus valores van acompañados de un carácter de escape, como reza la sintaxis de JSON.  
  
 Este es un ejemplo que muestra el formato de la salida JSON.  
  
 **Resultados de la consulta**  
  
|||||  
|-|-|-|-|  
|**A**|**B**|**C**|**D**|  
|10|11|12|X|  
|20|21|22|S|  
|30|31|32|Z|  
  
 **Salida JSON**  
  
```json  
[  
  { "A":10, "B":11, "C":12, "D":"X" },  
  { "A":20, "B":21, "C":22, "D":"Y" },  
  { "A":30, "B":31, "C":32, "D":"Z" }  
]  
```  
  
## Más información sobre FOR JSON y la compatibilidad integrada de JSON en SQL Server  
 [Entradas de blog del administrador de programas de Microsoft Jovan Popovic](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## Vea también  
 [Cláusula FOR &#40;Transact-SQL&#41;](../Topic/FOR%20Clause%20\(Transact-SQL\).md)   
 [Uso de salidas FOR JSON en SQL Server y en aplicaciones cliente &#40;SQL Server&#41;](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  