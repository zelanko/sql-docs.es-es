---
title: "Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la b&#250;squeda de texto completo | Microsoft Docs"
ms.custom: ""
ms.date: "02/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "listas de palabras irrelevantes [búsqueda de texto completo]"
  - "búsqueda de texto completo [SQL Server], lista de palabras irrelevantes"
  - "búsqueda de texto completo [SQL Server], palabras irrelevantes"
  - "palabras irrelevantes [búsqueda de texto completo]"
  - "búsqueda de texto completo [SQL Server], palabras irrelevantes"
  - "palabras irrelevantes [búsqueda de texto completo]"
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
caps.latest.revision: 81
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 79
---
# Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la b&#250;squeda de texto completo
  Para evitar que un índice de texto completo se llene demasiado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone de un mecanismo que descarta las cadenas más frecuentes que no ayudan en la búsqueda. Estas cadenas descartadas se denominan *palabras irrelevantes*. Durante la creación de índices, el motor de texto completo omite las palabras irrelevantes del índice de texto completo. Eso significa que las consultas de texto completo no buscarán las palabras irrelevantes.  
  
##  <a name="understand"></a> Descripción de palabras irrelevantes y listas de palabras irrelevantes  
 Una palabra irrelevante puede ser una palabra con significado en un idioma determinado o un *token* sin significado lingüístico. Por ejemplo, en inglés, las palabras como "a", "and", "is" y "the" se omiten en el índice de texto completo porque se ha determinado que no son útiles en una búsqueda.  
  
 Aunque omite la inclusión de palabras irrelevantes, el índice de texto completo tiene en cuenta la posición de las mismas.. Tomemos como ejemplo la frase en inglés "Instructions are applicable to these Adventure Works Cycles models ". La siguiente tabla muestra la posición de las palabras en la frase:  
  
|Word|Posición|  
|----------|--------------|  
|Instructions|1|  
|are|2|  
|applicable|3|  
|en|4|  
|these|5|  
|Adventure|6|  
|Works|7|  
|Cycles|8|  
|modelos|9|  
  
 Las palabras irrelevantes "are", "to" y "these" que se encuentran en las posiciones 2, 4 y 5 quedan excluidas del índice de texto completo. Sin embargo, se mantiene la información de su posición y, de este modo, no se ve afectada la posición de las demás palabras de la frase.  
  
 Las palabras irrelevantes se administran en bases de datos mediante objetos denominados listas de palabras irrelevantes. Una *lista de palabras irrelevantes* es una lista de palabras que, cuando se asocia a un índice de texto completo, se aplica a las consultas de texto completo en ese índice.  
  
 [En este tema](#TOP)  
  
##  <a name="creating"></a> Crear una lista de palabras irrelevantes  
 Puede crear una lista de palabras irrelevantes de cualquiera de las maneras siguientes:  
  
-   Usar la lista de palabras irrelevantes proporcionada por el sistema en la base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se distribuye con una lista de palabras irrelevantes del sistema que contiene las palabras irrelevantes usadas normalmente para cada idioma compatible; es decir, para cada idioma que está asociado de forma predeterminada a determinados separadores de palabras. La lista de palabras irrelevantes del sistema contiene palabras irrelevantes de uso común en todos los idiomas admitidos.  Puede copiar la lista de palabras irrelevantes del sistema y personalizar la copia agregando y quitando palabras irrelevantes.  
  
     La lista de palabras irrelevantes del sistema se instala en la base de datos [Resource](../../relational-databases/databases/resource-database.md) .  
  
-   Crear una lista propia de palabras irrelevantes y agregar a ella palabras irrelevantes para cualquier idioma que especifique. También puede quitar palabras de la lista de palabras irrelevantes cuando sea necesario.  
  
-   Usar una lista de palabras irrelevantes personalizada de cualquier otra base de datos en la instancia del servidor actual, y agregar y quitar palabras cuando sea necesario.  
  
 **Para crear una lista de palabras irrelevantes**  
  
-   [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)  
  
#### Para crear una lista de palabras irrelevantes de texto completo en Management Studio  
  
1.  En el Explorador de objetos, expanda el servidor.  
  
2.  Expanda **Bases de datos** y luego la base de datos en la que quiere crear la lista de palabras irrelevantes de texto completo.  
  
3.  Expanda **Almacenamiento** y luego haga clic con el botón derecho en **Lista de palabras irrelevantes de texto completo**.  
  
4.  Seleccione **Nueva lista de palabras irrelevantes de texto completo**.  
  
5.  Especifique el nombre de la lista de palabras irrelevantes.  
  
6.  Opcionalmente, especifique a otra persona como propietario de la lista de palabras irrelevantes.  
  
7.  Seleccione una de las opciones de creación de lista de palabras irrelevantes siguientes:  
  
    -   **Crear una lista de palabras irrelevantes vacía**  
  
    -   **Crear a partir de la lista de palabras irrelevantes del sistema**  
  
    -   **Crear a partir de una lista de palabras irrelevantes de texto completo existente**  
  
     Para obtener más información, vea [Nueva lista de palabras irrelevantes de texto completo &#40;página General&#41;](../Topic/New%20Full-Text%20Stoplist%20\(General%20Page\).md).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 **Para quitar una lista de palabras irrelevantes**  
  
-   [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-stoplist-transact-sql.md)  
  
 [En este tema](#TOP)  
  
##  <a name="queries"></a> Usar una lista de palabras irrelevantes en consultas de texto completo  
 Para usar una lista de palabras irrelevantes en consultas, es necesario asociarla a un índice de texto completo. Puede asociar una lista de palabras irrelevantes a un índice de texto completo en el momento de crear el índice, o puede modificar el índice más adelante y agregarle una lista de palabras irrelevantes.  
  
 **Para crear un índice de texto completo y asociarle una lista de palabras irrelevantes**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
 **Para asociar o desasociar una lista de palabras irrelevantes y un índice de texto completo existente**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
 **Para suprimir un mensaje de error si las palabras irrelevantes causan error en una operación booleana en una consulta de texto completo**  
  
-   [transform noise words (opción de configuración del servidor)](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)  
  
 [En este tema](#TOP)  
  
##  <a name="viewing"></a> Ver listas de palabras irrelevantes y sus metadatos  
 **Para ver todas las palabras de una lista de palabras irrelevantes**  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
 **Para obtener información sobre todas las listas de palabras irrelevantes de la base de datos actual**  
  
-   [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
-   [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
 **Para ver el resultado de la tokenización de una combinación entre un separador de palabras, un diccionario de sinónimos y una lista de palabras irrelevantes**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md)  
  
 [En este tema](#TOP)  
  
##  <a name="change"></a> Cambiar las palabras irrelevantes de una lista de palabras irrelevantes  
 **Para agregar o quitar palabras irrelevantes de una lista de palabras irrelevantes**  
  
-   [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)  
  
#### Para cambiar las palabras irrelevantes de una lista de palabras irrelevantes en Management Studio  
  
1.  En el Explorador de objetos, expanda el servidor.  
  
2.  Expanda **Bases de datos**y, a continuación, expanda la base de datos.  
  
3.  Expanda **Almacenamiento**y, a continuación, seleccione **Listas de palabras irrelevantes de texto completo**.  
  
4.  Haga clic con el botón derecho en la lista de palabras irrelevantes cuyas propiedades quiere cambiar y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo [Propiedades de lista de palabras irrelevantes de texto completo](../Topic/Full-Text%20Stoplist%20Properties.md):  
  
    1.  En el cuadro de lista **Acción** , seleccione una las acciones siguientes: **Agregar palabra irrelevante**, **Eliminar palabra irrelevante**, **Eliminar todas las palabras irrelevantes**o **Borrar lista de palabras irrelevantes**.  
  
    2.  Si el cuadro de texto **Palabra irrelevante** está habilitado para la acción seleccionada, escriba una única palabra irrelevante. Esta palabra irrelevante debe ser única; es decir, no debe estar todavía en esta lista de palabras irrelevantes para el idioma que seleccione.  
  
    3.  Si el cuadro de lista **Idioma de texto completo** está habilitado para la acción seleccionada, seleccione un idioma.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 [En este tema](#TOP)  
  
##  <a name="upgrade"></a> Actualizar las palabras irrelevantes de SQL Server 2005  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Cuando una base de datos se actualiza desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], los archivos de palabras irrelevantes de esa versión dejan de usarse. Sin embargo, los archivos de palabras irrelevantes están almacenados en la carpeta FTDATA\ FTNoiseThesaurusBak y se pueden usar posteriormente al actualizar o compilar las listas de palabras irrelevantes correspondientes. Para obtener información sobre cómo actualizar los archivos de palabras irrelevantes a listas de palabras irrelevantes, vea [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
 [En este tema](#TOP)  
  
  