---
title: Configurar y administrar archivos de sinónimos para búsquedas de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], configuring
- thesaurus [full-text search]
ms.assetid: 3ef96a63-8a52-45be-9a1f-265bff400e54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3a6d6197cb525ba4ad395da590ea113bdd0a1f0c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220345"
---
# <a name="configure-and-manage-thesaurus-files-for-full-text-search"></a>Configurar y administrar archivos de sinónimos para búsquedas de texto completo
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consultas de texto completo pueden buscar sinónimos de los términos especificados por el usuario mediante el uso de un diccionario de sinónimos. Un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *sinónimos* define un conjunto de sinónimos para un idioma específico. Los administradores del sistema pueden definir dos formatos de sinónimos: conjuntos de expansión y conjuntos de reemplazo. Al desarrollar un diccionario de sinónimos personalizado para los datos de texto completo, puede ampliar de forma eficaz el ámbito de las consultas de texto completo en esos datos. Coincidencia de diccionario de sinónimos tiene lugar para todas [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) y [FREETEXTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) consultas y para cualquier [CONTAINS](/sql/t-sql/queries/contains-transact-sql) y [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) consultas que Especifique la cláusula FORMSOF THESAURUS.  
  
##  <a name="tasks"></a> Tareas básicas para la configuración de un archivo de diccionario de sinónimos  
 Para que las consultas de búsqueda de texto completo en la instancia de servidor puedan buscar sinónimos en un idioma determinado, debe definir las asignaciones del diccionario de sinónimos de ese idioma. Cada diccionario de sinónimos se debe configurar manualmente para definir lo siguiente:  
  
-   Configuración de signos diacríticos  
  
     En un diccionario de sinónimos determinado, todos los patrones de búsqueda distinguen o no las marcas diacríticas como la tilde (**~**), la marca de acento agudo (**´**) o la diéresis (**¨**) (es decir, *distinguen acentos* o *no distinguen acentos*). Por ejemplo, imagine que especifica el patrón "café" para que sea reemplazado por otros patrones en una consulta de búsqueda de texto completo. Si el archivo de sinónimos no distingue acentos, la búsqueda de texto completo reemplaza los patrones "café" y "cafe". Si el archivo de sinónimos distingue acentos, la búsqueda de texto completo solo reemplaza el patrón "café". De forma predeterminada, un diccionario de sinónimos no distingue acentos.  
  
-   Conjunto de expansión  
  
     Un conjunto de expansión contiene un grupo de sinónimos como "escritor", "autor" y "periodista" que se sustituyen entre si en una consulta de texto completo. Las consultas que contienen una coincidencia para algún sinónimo en un conjunto de expansión se expanden para incluir uno de cada dos sinónimos en el conjunto de expansión.  
  
     Para obtener más información, vea "Estructura XML de un conjunto de expansión", posteriormente en este tema.  
  
-   Conjunto de reemplazo  
  
     Un conjunto de reemplazo contiene un patrón de texto que se reemplazará por un conjunto de sustitución. Para obtener un ejemplo, vea la sección "Estructura XML de un conjunto de reemplazo" más adelante en este tema.  
  
  
##  <a name="initial_thesaurus_files"></a> Contenido inicial de los archivos de sinónimos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un conjunto de archivos de sinónimos XML, uno para cada idioma admitido. Estos archivos están esencialmente vacíos. Contienen solo la estructura XML de nivel superior que es común a todos los diccionarios de sinónimos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un diccionario de sinónimos de ejemplo como comentario.  
  
 Los archivos de sinónimos que se publican con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contienen el siguiente código XML:  
  
```  
<XML ID="Microsoft Search Thesaurus">  
  
<!--  Commented out  
  
    <thesaurus xmlns="x-schema:tsSchema.xml">  
<diacritics_sensitive>0</diacritics_sensitive>  
        <expansion>  
            <sub>Internet Explorer</sub>  
            <sub>IE</sub>  
            <sub>IE5</sub>  
        </expansion>  
        <replacement>  
            <pat>NT5</pat>  
            <pat>W2K</pat>  
            <sub>Windows 2012</sub>  
        </replacement>  
        <expansion>  
            <sub>run</sub>  
            <sub>jog</sub>  
        </expansion>  
    </thesaurus>  
-->  
</XML>  
```  
  
  
##  <a name="location"></a> Ubicación de los archivos de diccionario de sinónimos  
 La ubicación predeterminada de los archivos de sinónimos es la siguiente:  
  
 *< SQL_Server_data_files_path >* \MSSQL12. MSSQLSERVER\MSSQL\FTDATA\  
  
 Esta ubicación predeterminada contiene los archivos siguientes:  
  
-   Archivos de sinónimos específicos del idioma  
  
     Durante la instalación, los archivos de sinónimos vacíos se instalan en la ubicación anterior. Se proporciona un archivo independiente para cada idioma admitido. Un administrador del sistema puede personalizar estos archivos.  
  
     Los nombres de archivo predeterminados de los archivos de sinónimos usan el formato siguiente:  
  
     'ts' + \<abreviatura de idioma de tres letras > + 'XML'  
  
     El nombre del archivo de diccionario de sinónimos para un idioma dado se especifica en el Registro en el valor siguiente: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<instance-name>\MSSearch\\<language-abbrev>.  
  
-   El archivo de sinónimos global  
  
     Un archivo de sinónimos global y vacío, tsGlobal.xml.  
  
 Puede cambiar la ubicación y los nombres de un archivo de sinónimos cambiando su clave del Registro. Para cada idioma, la ubicación del archivo de sinónimos se especifica en el valor siguiente en el Registro:  
  
 HKLM/SOFTWARE/Microsoft/Microsoft SQL Server /\<nombre de instancia>/MSSearch/Language/\<abreviatura_de_idioma > / TsaurusFile  
  
 El archivo de sinónimos global corresponde al idioma neutro con el LCID 0. Solo los administradores pueden cambiar este valor.  
  
  
##  <a name="how_queries_use_tf"></a> Cómo los archivos de diccionario de sinónimos de uso de consultas  
 Una consulta del diccionario de sinónimos utiliza un diccionario de sinónimos específico del idioma y el diccionario de sinónimos global. Primero, la consulta busca el archivo específico del idioma y lo carga para su procesamiento (a menos que ya esté cargado). La consulta se expande para incluir los sinónimos específicos del idioma especificados por las reglas de conjuntos de expansión y conjuntos de reemplazo en el archivo de diccionario de sinónimos. Estos pasos se repiten después para el diccionario de sinónimos global. Sin embargo, si un término ya forma parte de una coincidencia en el archivo de diccionario de sinónimos específico del idioma, el término es ilegible para coincidencias en el diccionario de sinónimos global.  
  
  
##  <a name="structure"></a> Descripción de la estructura de un archivo de diccionario de sinónimos  
 Cada archivo de diccionario de sinónimos define un contenedor XML cuyo identificador es `Microsoft Search Thesaurus`y un comentario, `<!--` ... `-->`, que contiene un diccionario de sinónimos de ejemplo. El diccionario de sinónimos se define en un \<sinónimos > elemento que contiene ejemplos de los elementos secundarios que definen la configuración de signos diacríticos, conjuntos de expansión y conjuntos de reemplazo, como sigue:  
  
-   Estructura XML de la configuración de signos diacríticos  
  
     La configuración de signos diacríticos de un diccionario de sinónimos se especifica en un único elemento <diacritics_sensitive>. Este elemento contiene un valor entero que controla la distinción de acentos, de la forma siguiente:  
  
    |Configuración de signos diacríticos|Valor|XML|  
    |------------------------|-----------|---------|  
    |no distinguen acentos|0|`<diacritics_sensitive>0</diacritics_sensitive>`|  
    |distinguen acentos|1|`<diacritics_sensitive>1</diacritics_sensitive>`|  
  
    > [!NOTE]  
    >  Esta configuración solo se puede aplicar una vez en el archivo, y se aplica a todos los patrones de búsqueda del mismo. Esta configuración no se puede especificar para patrones individuales.  
  
-   Estructura XML de un conjunto de expansión  
  
     Cada conjunto de expansión está delimitado por un \<expansión > elemento. Dentro de este elemento, se especifican uno o más sustituciones en un \<sub > elemento. En el conjunto de expansión, puede especificar un grupo de sustituciones que sean sinónimas.  
  
     Por ejemplo, puede editar la sección de expansión para tratar las sustituciones "writer", "author" y "journalist" como sinónimos. Las consultas de búsqueda de texto completo que contienen coincidencias en una sustitución se expanden para incluir todas las demás sustituciones especificadas en el conjunto de expansión. Por tanto, en el ejemplo anterior, al emitir una consulta FORMS OF THESAURUS o FREETEXT para la palabra "autor", la búsqueda de texto completo también devuelve resultados que contienen las palabras "escritor" y "periodista".  
  
     Esta es la apariencia que tendrá la sección del conjunto de expansión en el caso del ejemplo anterior:  
  
    ```  
    <expansion>  
            <sub>writer</sub>  
            <sub>author</sub>  
            <sub>journalist</sub>  
    </expansion>  
    ```  
  
-   Estructura XML de un conjunto de reemplazo  
  
     Cada conjunto de reemplazo está delimitado por un \<reemplazo > elemento. Dentro de este elemento puede especificar uno o varios modelos en un \<pat > elemento y cero o más sustituciones en \<sub > elementos, uno por cada sinónimo. Puede especificar un patrón para que sea reemplazado por un conjunto de sustitución. Los patrones y las sustituciones pueden contener una palabra o una secuencia de palabras. Si no se especifica ninguna sustitución para un modelo, se quita el modelo de la consulta del usuario.  
  
     Por ejemplo, imagine que desea que las consultas de "Win8", el patrón, sean reemplazadas por "Windows Server 2012" o "Windows 8.0", las sustituciones. Si ejecuta una búsqueda de texto completo de "Win8", solo devolverá los resultados que contengan "Windows Server 2012" o "Windows 8.0". No devolverá resultados que contengan "Win8". Esto se debe a que el patrón "Win8" ha sido "reemplazado" por los patrones "Windows Server 2012" y "Windows 8.0".  
  
     Éste es el aspecto que tendrá la sección del conjunto de reemplazo en el caso del ejemplo anterior:  
  
    ```  
    <replacement>  
            <pat>Win8</pat>  
            <sub>Windows Server 2012</sub>  
            <sub>Windows 8.0</sub>  
    </replacement>  
    ```  
  
     Si tiene dos conjuntos de reemplazo con patrones similares para los que se buscan coincidencias, prevalecerá el más largo de los dos. Por ejemplo, si ejecuta una consulta FORMS OF THESAURUS para "Comunidad en línea de Internet Explorer" y tiene los siguientes conjuntos de reemplazo, el conjunto de reemplazo "Internet Explorer" tiene prioridad sobre el conjunto de reemplazo "Internet". Por tanto, la consulta se procesará como "Comunidad en línea de IE" o "Comunidad en línea de IE 9".  
  
    ```  
    <replacement>  
             <pat>Internet</pat>  
             <sub>intranet</sub>  
    </replacement>  
    ```  
  
     y  
  
    ```  
    <replacement>  
             <pat>Internet Explorer</pat>  
             <sub>IE</sub>  
             <sub>IE 9</sub>  
    </replacement>  
    ```  
  
  
##  <a name="working_with_thesaurus_files"></a> Trabajar con archivos de sinónimos  
 **Para editar un archivo de diccionario de sinónimos**  
  
-   [Editar un archivo de diccionario de sinónimos](#editing)  
  
 **Para cargar un archivo de diccionario de sinónimos actualizado**  
  
-   [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql)  
  
 **Para ver el resultado de la tokenización de una combinación de separador de diccionario de sinónimos y lista de palabras irrelevantes de word**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
  
##  <a name="editing"></a> Editar un archivo de diccionario de sinónimos  
 El diccionario de sinónimos de un idioma determinado se puede configurar modificando su archivo de diccionario de sinónimos (un archivo XML). Durante la instalación, vaciar archivos de sinónimos que solo contienen la \<xml > contenedor y un ejemplo comentado \<sinónimos > elemento están instalados. Consultas de búsqueda de texto completo que buscan sinónimos funcionen correctamente, debe crear un real \<sinónimos > elemento que define un conjunto de sinónimos. Puede definir dos formatos de sinónimos: conjuntos de expansión y conjuntos de reemplazo.  
  
 **Restricciones para los archivos de sinónimos**  
  
 Las restricciones siguientes se aplican al modificar un archivo de diccionario de sinónimos:  
  
-   Solo los administradores del sistema pueden actualizar, modificar o eliminar archivos de diccionarios de sinónimos.  
  
-   Al modificar archivos de diccionarios de sinónimos con herramientas de edición de texto, los archivos deben guardarse en formato Unicode y deben especificarse marcas de orden de bytes.  
  
-   Las entradas del diccionario de sinónimos no pueden estar vacías ni tener separación de palabras en una cadena vacía.  
  
-   Las frases del archivo de diccionario de sinónimos no deben tener más de 512 caracteres.  
  
-   Un diccionario de sinónimos no debe contener ninguna entrada duplicada entre las \<sub > entradas de conjuntos de expansión y la \<pat > elementos de conjuntos de reemplazo.  
  
 **Recomendaciones para los archivos de sinónimos**  
  
 Se recomienda que las entradas del archivo de diccionario de sinónimos no contengan ningún carácter especial. Esto se debe a que los separadores de palabras demuestran comportamientos sutiles con respecto a los caracteres especiales. Si una entrada del diccionario de sinónimos contiene algún carácter especial, los separadores de palabras que se usan en combinación con esa entrada pueden tener implicaciones sutiles de comportamiento en una consulta de texto completo.  
  
 Se recomienda que \<sub > entradas no contengan palabras irrelevantes porque las palabras irrelevantes se omiten en el índice de texto completo. Las consultas se expanden para incluir el \<sub > entradas desde un archivo de diccionario de sinónimos y si un \<sub > entrada contiene palabras irrelevantes, el tamaño de la consulta aumenta innecesariamente.  
  
#### <a name="to-edit-a-thesaurus-file"></a>Modificar un archivo de sinónimos  
  
1.  Abra el archivo de diccionario de sinónimos en el Bloc de notas.  
  
2.  Si va a modificar el archivo de sinónimos por primera vez, quite las siguientes líneas de comentarios del principio y el final del archivo, respectivamente:  
  
    ```  
    <!--Commented out  
    -->  
    ```  
  
3.  Agregue, modifique o elimine un conjunto de reemplazo o un conjunto de expansión.  
  
4.  Guarde el archivo y cierre el Bloc de notas.  
  
5.  Use [sp_fulltext_load_thesaurus_file](/sql/relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql) para cargar el contenido del archivo de diccionario de sinónimos en tempdb, especificando el identificador local (LCID) que corresponde al idioma del archivo de diccionario de sinónimos. Por ejemplo, para el archivo de diccionario de sinónimos en inglés, tsenu.xml, el LCID correspondiente es 1033.  
  
    ```  
    USE AdventureWorks2012 ;  
    EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
    GO  
    ```  
  
  
## <a name="see-also"></a>Vea también  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [Búsqueda de texto completo](full-text-search.md)  
  
  
