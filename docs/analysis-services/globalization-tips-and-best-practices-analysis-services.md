---
title: Sugerencias de globalización y procedimientos recomendados (Analysis Services) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57031c75e9433981b45419348ab2d5c0745edbfd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62659499"
---
# <a name="globalization-tips-and-best-practices-analysis-services"></a>Sugerencias de globalización y procedimientos recomendados (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  [!INCLUDE[applies](../includes/applies-md.md)] Solo multidimensional  
  
 Con estas sugerencias e instrucciones, le resultará más fácil aumentar la portabilidad de las soluciones de inteligencia empresarial y evitar errores que están directamente relacionados con la configuración de idioma e intercalación.  
  
##  <a name="bkmk_sameColl"></a> Usar intercalaciones similares en toda la pila  
 Si es posible, trate de utilizar la misma configuración de intercalación en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y en el motor de base de datos, para que la distinción de ancho, la distinción entre mayúsculas y minúsculas y la distinción de acceso sean iguales.  
  
 La intercalación de cada servicio tiene su propia configuración, con el valor predeterminado del motor de la base de datos establecido en SQL_Latin1_General_CP1_CI_AS y con Analysis Services establecido en Latin1_General_AS. Los valores predeterminados son compatibles en términos de distinción de mayúsculas y minúsculas, ancho y acentos. Tenga en cuenta que si cambia la configuración de intercalaciones en uno de estos elementos, pueden surgir problemas cuando las propiedades de intercalación difieran en aspectos fundamentales.  
  
 Aunque la configuración de intercalación tenga funciones equivalentes, puede encontrarse con un caso especial en el que cada servicio interprete de manera distinta un espacio vacío en algún lugar de una cadena.  
  
 El carácter de espacio es un “caso especial” porque se puede representar como un juego de caracteres de byte único (SBCS) o de doble byte (DBCS) en Unicode. En el motor relacional, dos cadenas compuestas separadas por un espacio, una en SBCS y la otra en DBCS, se consideran idénticas. En Analysis Services, durante el procesamiento, las dos cadenas compuestas no son idénticas, y la segunda instancia se marcará como duplicado.  
  
 Para ver más detalles y las soluciones alternativas sugeridas, consulte el tema sobre [espacios en blanco en una cadena Unicode que tienen resultados de procesamiento diferentes en función de la intercalación](http://social.technet.microsoft.com/wiki/contents/articles/23979.ssas-processing-error-blanks-in-a-unicode-string-have-different-processing-outcomes-based-on-collation-and-character-set.aspx).  
  
##  <a name="bkmk_recos"></a> Recomendaciones de intercalación comunes  
 Analysis Services siempre muestra la lista completa de todos los idiomas e intercalaciones disponibles; no filtra las intercalaciones según el idioma seleccionado. Asegúrese de elegir una combinación factible.  
  
 Algunas de las intercalaciones más comúnmente usadas son las de la lista siguiente.  
  
 Debe considerar esta lista como un punto de partida para una investigación más detallada y no como una recomendación definitiva que excluya otras opciones. Puede ser que una intercalación no específicamente recomendada sea la más adecuada para sus datos. La única forma de comprobar si los valores de datos se ordenan y comparan adecuadamente es realizar pruebas minuciosas. Como siempre, asegúrese de ejecutar las cargas de trabajo tanto de procesamiento como de consulta al probar la intercalación.  
  
-   Latin1_General_100_AS se suele usar para las aplicaciones que usan los 26 caracteres del [alfabeto ISO de latín básico](http://en.wikipedia.org/wiki/ISO_basic_Latin_alphabet).  
  
-   Los idiomas de Europa del Norte que utilizan letras escandinavas (como ø) pueden utilizar Finnish_Swedish_100.  
  
-   Los idiomas de la Europa del Este, como el ruso, a menudo usan Cyrillic_General_100.  
  
-   Las intercalaciones y el idioma chino varían según la región, pero normalmente se utiliza el chino simplificado o el chino tradicional.  
  
     En RPC y Singapur, Microsoft Support acostumbra a preferir el chino simplificado con pinyin como orden de clasificación. Las intercalaciones recomendadas son Chinese_PRC (para SQL Server 2000), Chinese_PRC_90 (para SQL Server 2005) o Chinese_Simplified_Pinyin_100 (para SQL Server 2008 y versiones posteriores).  
  
     En Taiwán, es más habitual ver chino tradicional con el criterio de ordenación recomendado se basa en el número de trazos: Chinese_Taiwan_Stroke (para SQL Server 2000), Chinese_Taiwan_Stroke_90 (para SQL Server 2005) o Chinese_Traditional_Stroke_Count_100 (para SQL Server 2008 y versiones posteriores).  
  
     Otras regiones (por ejemplo, Hong Kong y Macao) también utilizan el chino tradicional. Para las intercalaciones en Hong Kong es habitual ver Chinese_Hong_Kong_Stroke_90 (en SQL Server 2005). En Macao, se utiliza con bastante frecuencia Chinese_Traditional_Stroke_Count_100 (en SQL Server 2008 y versiones posteriores).  
  
-   Para el japonés, la intercalación utiliza con más frecuencia es Japanese_CI_AS. Japanese_XJIS_100 se usa en instalaciones que admiten [JIS2004](http://en.wikipedia.org/wiki/JIS_X_0213). Japanese_BIN2 suele aparecer en proyectos de migración de datos, con datos que se originan en plataformas que no son de Windows o en orígenes de datos distintos al motor de base de datos relacional de SQL Server.  
  
     Japanese_Bushu_Kakusu_100 raramente aparece en servidores que ejecutan cargas de trabajo de Analysis Services.  
  
-   Para el coreano se recomienda Korean_100. Aunque en la lista sigue apareciendo Korean_Wansung_Unicode, ya no se utiliza.  
  
##  <a name="bkmk_objid"></a> Distinción entre mayúsculas y minúsculas de los identificadores de objetos  
 Desde SQL Server 2012 SP2, la distinción entre mayúsculas y minúsculas de los identificadores de objetos se exige independientemente de la intercalación, pero el comportamiento varía según el idioma:  
  
|Alfabeto del idioma|Distinción de mayúsculas y minúsculas|  
|---------------------|----------------------|  
|**Alfabeto Latín básico**|Los identificadores de objetos expresados en el alfabeto latino (cualquiera de las 26 letras mayúsculas o minúsculas del inglés) se tratan sin distinguir mayúsculas de minúsculas, independientemente de la intercalación. Por ejemplo, los identificadores de objeto siguientes se consideran idénticos: 54321**abcdef**, 54321**ABCDEF**, 54321**AbCdEf**. Internamente, Analysis Services trata los caracteres de la cadena como si todos estuvieran en mayúsculas y, luego, realiza una comparación de byte simple que es independiente del idioma.<br /><br /> Tenga en cuenta que solo los 26 caracteres se ven afectados. Si el idioma es Europeo occidental pero utiliza caracteres escandinavos, los caracteres adicionales no estarán en mayúsculas.|  
|**Cirílico, griego, copto y armenio**|Los identificadores de objetos en script bicameral no latino, como el cirílico, siempre distinguen entre mayúsculas y minúsculas. Por ejemplo, Измерение y измерение se consideran dos valores distintos, aunque la única diferencia sea el uso de mayúsculas y minúsculas en la primera letra.|  
  
 **Implicaciones de la distinción entre mayúsculas y minúsculas para los identificadores de objetos**  
  
 Solo los identificadores de objetos, y no los nombres de objetos, están sujetos a los comportamientos de mayúsculas y minúsculas que se describen en la tabla. Si ve un cambio en el funcionamiento de la solución (una comparación del antes y el después de instalar SQL Server 2012 SP2 o una versión posterior), probablemente se trate de un problema de procesamiento. Las consultas no se ven afectadas por los identificadores de objeto. En los dos lenguajes de consulta (DAX y MDX), el motor de fórmulas utiliza el nombre del objeto (no el identificador).  
  
> [!NOTE]  
>  Los cambios de código relacionados con la distinción entre mayúsculas y minúsculas han supuesto un cambio importante para algunas aplicaciones. Para obtener más información, vea [Cambios recientes en las características de Analysis Services en SQL Server 2016](../analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2016.md) .  
  
##  <a name="bkmk_test"></a> Pruebas de configuración regional con Excel, SQL Server Profiler y SQL Server Management Studio  
 Al probar las traducciones, la conexión debe especificar el LCID de la traducción. Como se documenta en el tema sobre [cómo obtener otro idioma de SSAS en Excel](http://extremeexperts.com/sql/Tips/ExcelDiffLocale.aspx), puede utilizar Excel para probar las traducciones.  
  
 Puede hacerlo manualmente, editando el archivo .odc para incluir la propiedad de cadena de conexión del identificador de configuración regional. Pruebe con la base de datos multidimensional de muestra de Adventure Works.  
  
-   Busque los archivos .odc existentes. Cuando encuentre el de la base de datos multidimensional de Adventure Works, haga clic con el botón derecho en el archivo para abrirlo en el Bloc de notas.  
  
-   Agregue `Locale Identifier=1036` a la cadena de conexión. Guarde el archivo y ciérrelo.  
  
-   Abra Excel | **Datos** | **Conexiones existentes**. Filtre la lista para que solo aparezcan los archivos de las conexiones de este equipo. Busque la conexión de Adventure Works (observe el nombre con atención: puede que haya más de una). Abra la conexión.  
  
     Debería ver las traducciones al francés de la base de datos de muestra de Adventure Works.  
  
     ![Tabla dinámica de Excel con traducciones al francés](../analysis-services/media/ssas-localetest-excel.png "tabla dinámica de Excel con traducciones al francés")  
  
 A modo de seguimiento, puede usar SQL Server Profiler para confirmar la configuración regional. Haga clic en un evento de `Session Initialize` y, luego, observe la lista de propiedades del área de texto inferior para buscar `<localeidentifier>1036</localeidentifier>`.  
  
 En Management Studio, puede especificar el identificador de configuración regional en una conexión de servidor.  
  
-   En el Explorador de objetos | **Conectar** | **Analysis Services** | **Opciones**, haga clic en la pestaña **Parámetros de conexión adicionales** .  
  
-   Escriba `Local Identifier=1036` y, después, haga clic en **Conectar**.  
  
-   Ejecute una consulta MDX en la base de datos de Adventure Works. Los resultados de la consulta deberían ser las traducciones al francés.  
  
     ![Consulta MDX con traducciones al francés en SSMS](../analysis-services/media/ssas-localetest-ssms.png "consulta MDX con traducciones al francés en SSMS")  
  
##  <a name="bkmk_mdx"></a> Escritura de consultas MDX en una solución que contiene traducciones  
 Las traducciones proporcionan información de los nombres de los objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , pero los identificadores de los mismos objetos no se traducen. Siempre que sea posible, utilice los identificadores y las claves de los objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en lugar de los títulos y los nombres traducidos. Por ejemplo, utilice claves de miembro en lugar de nombres de miembro en los scripts e instrucciones MDX (Expresiones multidimensionales) con el fin de asegurar la portabilidad entre diferentes idiomas.  
  
> [!NOTE]  
>  Recuerde que los nombres de objetos tabulares siempre distinguen mayúsculas de minúsculas, independientemente de la intercalación. Los nombres del objeto multidimensional, en cambio, siguen la distinción entre mayúsculas y minúsculas de la intercalación. Puesto que solo los nombres de los objetos multidimensionales distinguen entre mayúsculas y minúsculas, compruebe que en todas las consultas MDX que hagan referencia a objetos multidimensionales se utilicen las mayúsculas y las minúsculas correctamente.  
  
##  <a name="bkmk_datetime"></a> Escritura de consultas MDX que contengan valores de fecha y hora  
 Las siguientes sugerencias permiten hacer que las consultas MDX basadas en el tiempo y en la fecha sean más portables en los diferentes idiomas:  
  
1.  **Utilizar elementos numéricos para las comparaciones y operaciones**  
  
     Cuando realice operaciones y comparaciones de día de la semana y mes, utilice los elementos numéricos de hora y fecha en lugar de los equivalentes de cadena (por ejemplo, utilice MonthNumberofYear en lugar de MonthName). Los valores numéricos se ven menos afectados por las diferencias en las traducciones de idiomas.  
  
2.  **Utilizar los equivalentes de cadena en un conjunto de resultados**  
  
     Al generar conjuntos de resultados vistos por los usuarios finales, plantéese la posibilidad de utilizar una cadena (como MonthName) para que la audiencia multilingüe pueda utilizar las traducciones proporcionadas.  
  
3.  **Usar formatos de fecha ISO para información de fecha y hora universal**  
  
     Una [experto en Analysis Services](http://geekswithblogs.net/darrengosbell/Default.aspx) tiene esta recomendación: "Siempre uso el ISO formato de fecha aaaa-mm-dd para todas las cadenas de fecha que paso a las consultas en SQL o MDX porque no es ambiguo y funciona independientemente del cliente o la configuración regional del servidor. Sé que el servidor debería recurrir a su configuración regional al analizar formatos de fecha ambiguos, pero también creo que si hay una opción que no da pie a varias interpretaciones, lo mejor es elegir esa opción en cualquier caso”.  
  
4.  **Use la función Format para aplicar un formato específico, con independencia de la configuración regional de idioma.**  
  
     La siguiente consulta MDX, extraída de una entrada de foro, muestra cómo utilizar el formato para devolver las fechas en un formato específico, independientemente de la configuración regional subyacente.  
  

    ```  
    WITH MEMBER [LinkTimeAdd11Date_Manual] as Format(dateadd("d",15,"2014-12-11"), "mm/dd/yyyy")  
    member [LinkTimeAdd15Date_Manual] as Format(dateadd("d",11,"2014-12-13"), "mm/dd/yyyy")  
    SELECT  
    { [LinkTimeAdd11Date_Manual]  
    ,[LinkTimeAdd15Date_Manual]  
    }  
    ON COLUMNS   
    FROM [Adventure Works]  
  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Escenarios de globalización para Analysis Services](../analysis-services/globalization-scenarios-for-analysis-services.md)   
 [Escribir instrucciones Transact-SQL internacionales](../relational-databases/collations/write-international-transact-sql-statements.md)  
  
  
