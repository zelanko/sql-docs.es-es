---
description: Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo
title: Configuración y administración de palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo
ms.date: 02/02/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], noise words
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 43b5ce7b-9f09-4443-8a5b-c3da6eb28bcc
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: 54c462ee83fe972eccc9347e8a9f41e570511239
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91869408"
---
# <a name="configure-and-manage-stopwords-and-stoplists-for-full-text-search"></a>Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Para evitar que un índice de texto completo se llene demasiado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone de un mecanismo que descarta las cadenas más frecuentes que no ayudan en la búsqueda. Estas cadenas descartadas se denominan *palabras irrelevantes*. Durante la creación de índices, el motor de texto completo omite las palabras irrelevantes del índice de texto completo. Eso significa que las consultas de texto completo no buscarán las palabras irrelevantes.  
   
**Palabras irrelevantes**. Una palabra irrelevante puede ser una palabra con significado en un idioma específico. Por ejemplo, en inglés, las palabras como "a", "and", "is" y "the" se omiten en el índice de texto completo porque se ha determinado que no son útiles en una búsqueda. Una palabra irrelevante también puede ser un *token* que carezca de significado lingüístico.  

**Listas de palabras irrelevantes**. Las palabras irrelevantes se administran en bases de datos mediante objetos denominados listas de palabras irrelevantes. Una *lista de palabras irrelevantes* es una lista de palabras que, cuando se asocia a un índice de texto completo, se aplica a las consultas de texto completo en ese índice.
   
## <a name="use-an-existing-stoplist"></a>Utilizar una listas de palabras irrelevantes existente  
 Puede utilizar una lista de palabras irrelevantes existente de las maneras siguientes:  
  
-   Usar la lista de palabras irrelevantes proporcionada por el sistema en la base de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se distribuye con una lista de palabras irrelevantes del sistema que contiene las palabras irrelevantes usadas normalmente para cada idioma compatible; es decir, para cada idioma asociado de forma predeterminada a determinados separadores de palabras. Puede copiar la lista de palabras irrelevantes del sistema y personalizar la copia agregando y quitando palabras irrelevantes.  
  
     La lista de palabras irrelevantes del sistema se instala en la base de datos [Resource](../../relational-databases/databases/resource-database.md) .  
  
-   Use una lista de palabras irrelevantes personalizada de otra base de datos en la instancia del servidor actual y luego agregue o quite palabras irrelevantes cuando sea necesario.  
  
## <a name="create-a-new-stoplist"></a>Crear una nueva lista de palabras irrelevantes 
### <a name="create-a-new-stoplist-with-transact-sql"></a>Crear una nueva lista de palabras irrelevantes con Transact-SQL
Use [CREATE FULLTEXT STOPLIST](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md).

### <a name="create-a-new-stoplist-with-management-studio"></a>Crear una nueva lista de palabras irrelevantes con Management Studio
  
1.  En el Explorador de objetos, expanda el servidor.  
  
2.  Expanda **Bases de datos**y luego la base de datos en la que quiere crear la lista de palabras irrelevantes de texto completo.  
  
3.  Expanda **Almacenamiento** y, a continuación, haga clic con el botón secundario en **Listas de palabras irrelevantes de texto completo**.  
  
4.  Seleccione **Nueva lista de palabras irrelevantes de texto completo**.  
  
5.  Escriba el nombre de la nueva lista de palabras irrelevantes.  
  
6.  Opcionalmente, especifique a otra persona como propietario de la lista de palabras irrelevantes.  
  
7.  Seleccione una de las opciones de creación de lista de palabras irrelevantes siguientes:  
  
    -   **Crear una lista de palabras irrelevantes vacía**  
  
    -   **Crear a partir de la lista de palabras irrelevantes del sistema**  
  
    -   **Crear a partir de una lista de palabras irrelevantes de texto completo existente**  
  
     Para obtener más información, vea [Nueva lista de palabras irrelevantes de texto completo &#40;página General&#41;](/previous-versions/sql/sql-server-2016/cc280518(v=sql.130)).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="use-a-stoplist-in-full-text-queries"></a>Usar una lista de palabras irrelevantes en consultas de texto completo  
 Para usar una lista de palabras irrelevantes en consultas, es necesario asociarla a un índice de texto completo. Puede asociar una lista de palabras irrelevantes a un índice de texto completo en el momento de crear el índice, o puede modificar el índice más adelante y agregarle una lista de palabras irrelevantes.  
  
### <a name="create-a-full-text-index-and-associate-a-stoplist-with-it"></a>Crear un índice de texto completo y asociarle una lista de palabras irrelevantes
Use [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).
  
### <a name="associate-or-disassociate-a-stoplist-with-an-existing-full-text-index"></a>Asociar o desasociar una lista de palabras irrelevantes y un índice de texto completo existente
Use [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md). 
  
## <a name="change-the-stopwords-in-a-stoplist"></a>Cambiar las palabras irrelevantes de una lista de palabras irrelevantes  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-transact-sql"></a>Agregue o quite palabras irrelevantes de una lista de palabras irrelevantes con Transact-SQL
Use [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md).
  
### <a name="add-or-drop-stopwords-from-a-stoplist-with-management-studio"></a>Agregue o quite palabras irrelevantes de una lista de palabras irrelevantes con Management Studio  
  
1.  En el Explorador de objetos, expanda el servidor.  
  
2.  Expanda **Bases de datos**y, a continuación, expanda la base de datos.  
  
3.  Expanda **Almacenamiento** y, a continuación, seleccione **Listas de palabras irrelevantes de texto completo**.  
  
4.  Haga clic con el botón derecho en la lista de palabras irrelevantes cuyas propiedades quiere cambiar y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo [Propiedades de lista de palabras irrelevantes de texto completo](/previous-versions/sql/sql-server-2016/cc280415(v=sql.130)) :  
  
    1.  En el cuadro de lista **Acción** , seleccione una las acciones siguientes: **Agregar palabra irrelevante**, **Eliminar palabra irrelevante**, **Eliminar todas las palabras irrelevantes**o **Borrar lista de palabras irrelevantes**.  
  
    2.  Si el cuadro de texto **Palabra irrelevante** está habilitado para la acción seleccionada, escriba una única palabra irrelevante. Esta palabra irrelevante debe ser única; es decir, no debe estar todavía en esta lista de palabras irrelevantes para el idioma que seleccione.  
  
    3.  Si el cuadro de lista **Idioma de texto completo** está habilitado para la acción seleccionada, seleccione un idioma.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="manage-stoplists-and-their-usage"></a>Administrar listas de palabras irrelevantes y su uso
  
### <a name="view-all-the-stopwords-in-a-stoplist"></a>Ver todas las palabras irrelevantes de una lista de palabras irrelevantes
Use [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md). 
  
### <a name="get-info-about-all-the-stoplists-in-the-current-database"></a>Obtener información sobre todas las listas de palabras irrelevantes de la base de datos actual
Utilice [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md) y  [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md).
  
### <a name="view-the-tokenization-result-of-a-word-breaker-thesaurus-and-stoplist-combination"></a>Ver el resultado de la tokenización de una combinación entre un separador de palabras, un diccionario de sinónimos y una lista de palabras irrelevantes
Utilice [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).

### <a name="suppress-an-error-message-if-stopwords-cause-a-boolean-operation-on-a-full-text-query-to-fail"></a>Suprimir un mensaje de error si las palabras irrelevantes causan error en una operación booleana en una consulta de texto completo
Utilice la [opción de configuración del servidor transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md). 
   
## <a name="more-info-about-stopword-position"></a>Más información sobre la posición de la palabra irrelevante
 Aunque omite la inclusión de palabras irrelevantes, el índice de texto completo tiene en cuenta la posición de las mismas. Tomemos como ejemplo la frase en inglés "Instructions are applicable to these Adventure Works Cycles models ". La siguiente tabla muestra la posición de las palabras en la frase:  
  
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
  
## <a name="upgrade-noise-words-from-sql-server-2005"></a>Actualizar las palabras irrelevantes de SQL Server 2005  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Cuando una base de datos se actualiza desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], los archivos de palabras irrelevantes de esa versión dejan de usarse. Sin embargo, los archivos de palabras irrelevantes están almacenados en la carpeta FTDATA\ FTNoiseThesaurusBak y se pueden usar posteriormente al actualizar o compilar las listas de palabras irrelevantes correspondientes. Para obtener información sobre cómo actualizar los archivos de palabras irrelevantes a listas de palabras irrelevantes, vea [Actualizar la búsqueda de texto completo](../../relational-databases/search/upgrade-full-text-search.md).  
  
  
