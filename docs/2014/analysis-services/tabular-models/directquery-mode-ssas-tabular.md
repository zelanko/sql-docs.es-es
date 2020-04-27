---
title: Modo DirectQuery (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.realtime.f1
ms.assetid: 45ad2965-05ec-4fb1-a164-d8060b562ea5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a9c1510030f61896f686b49f4bc134a7dfcb42b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67284873"
---
# <a name="directquery-mode-ssas-tabular"></a>Modo DirectQuery (SSAS tabular)
  El *modo DirectQuery*de Analysis Services le permite recuperar datos y crear informes de un modelo tabular recuperando los datos y agregándolos directamente desde un sistema de base de datos relacional. En este tema se presentan las diferencias entre los modelos tabulares estándar que residen únicamente en la memoria y los modelos tabulares que pueden realizar consultas en un origen de datos relacional, y se explica cómo crear e implementar un modelo para utilizar en el modo DirectQuery.  
  
 Secciones de este tema:  
  
-   [Ventajas del modo DirectQuery](#bkmk_Benefits)  
  
-   [Crear modelos para su uso con el modo DirectQuery](#bkmk_Design)  
  
    -   [Data Sources for DirectQuery Models](directquery-mode-ssas-tabular.md#bkmk_DataSources)  
  
    -   [Restricciones de validación y de diseño para el modo DirectQuery](#bkmk_Validation)  
  
    -   [Compatibilidad de las fórmulas para los modelos DirectQuery](#bkmk_FormulaCompat)  
  
    -   [La seguridad en el modo DirectQuery](#bkmk_Security)  
  
    -   [La seguridad en el modo DirectQuery](#bkmk_Security)  
  
-   [Propiedades de DirectQuery](#bkmk_PropertyList)  
  
-   [Temas y tareas relacionados](#bkmk_related_tasks)  
  
##  <a name="benefits-of-directquery-mode"></a><a name="bkmk_Benefits"></a>Ventajas del modo DirectQuery  
 De forma predeterminada, los modelos tabulares utilizan una caché en memoria para almacenar los datos y realizar consultas en ellos. Dado que los modelos tabulares utilizan datos que residen en memoria, incluso las consultas más complejas pueden resultar increíblemente rápidas. Sin embargo, el uso de datos en caché tiene algunas desventajas:  
  
-   Los datos no se actualizan cuando cambian los datos de origen. Es necesario procesar el modelo para conseguir actualizaciones de los datos.  
  
-   Cuando se apaga el equipo que hospeda el modelo, el contenido de la memoria caché se guarda en el disco y deberá abrirse de nuevo al cargar el modelo o abrir el archivo de PowerPivot. Las operaciones de guardado y de carga pueden requerir mucho tiempo.  
  
 En cambio, el modo DirectQuery utiliza los datos almacenados en una base de datos de SQL Server.  Normalmente, se importan todos los datos o una pequeña muestra de ellos en la memoria caché mientras se crea el modelo y, al implantarlo, se especifica que el origen de datos para las consultas realizadas en él debe ser SQL Server, no los datos en caché. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] traducirá cualquier consulta DAX de datos a instrucciones SQL equivalentes en el origen de datos relacional especificado.  
  
 La implantación de un modelo mediante el modo DirectQuery ofrece muchas ventajas:  
  
-   Es posible tener un modelo acerca de los conjuntos de datos que son demasiado grandes para caber en la memoria del servidor de Analysis Services.  
  
-   La actualización de los datos está garantizada, y no existe una sobrecarga adicional de administración al no tener que mantener otra copia de estos. Los cambios en el origen de datos subyacente se pueden reflejar inmediatamente en las consultas realizadas en el modelo de datos.  
  
-   DirectQuery puede beneficiarse de la aceleración de consultas del proveedor, como la proporcionada por los índices de columnas optimizadas de memoria xVelocity.  
  
-   La aplicación de la seguridad requerida por la base de datos back-end se garantiza mediante la seguridad de nivel de filas. En cambio, si usa datos en caché, puede resultar difícil garantizar que la memoria caché esté protegida exactamente como en el servidor.  
  
-   Si el modelo contiene fórmulas complejas que requieren varias consultas, Analysis Services puede realizar la optimización para asegurarse de que el plan de consulta para la consulta ejecutada en la base de datos back-end sea tan eficaz como sea posible.  
  
##  <a name="authoring-models-for-use-with-directquery-mode"></a><a name="bkmk_Design"></a>Crear modelos para su uso con el modo DirectQuery  
 Los modelos tabulares se crean mediante el diseñador de modelos [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. El diseñador crea todos los modelos en la memoria, lo que significa que cuando se realiza el modelado, si los datos no caben en la memoria, se debe importar solo un subconjunto de datos en la memoria caché utilizada por la base de datos del área de trabajo.  
  
 Cuando esté listo para cambiar al modo DirectQuery, puede cambiar una propiedad que habilite este modo. Para obtener más información, vea [Habilitar el modo de diseño de DirectQuery &#40;&#41;tabular de SSAS ](enable-directquery-mode-in-ssdt.md).  
  
 Al hacerlo, el diseñador de modelos configura automáticamente la base de datos del área de trabajo para que se ejecute en un modo híbrido que le permita continuar trabajando con los datos en caché. Asimismo, el diseñador de modelos le notificará acerca de las características del modelo que son incompatibles con el modo DirectQuery. En la lista siguiente se resumen los principales requisitos que se han de tener en cuenta:  
  
-   **Orígenes de datos:** Los modelos DirectQuery solo pueden utilizar datos de un único origen de datos de SQL Server. Cuando se ha activado el modo DirectQuery para un modelo, no se puede utilizar ningún otro tipo de datos del diseñador de modelos, incluidas las tablas agregadas por operaciones de cortar y pegar. El resto de las opciones de importación están deshabilitadas. Todas las tablas incluidas en una consulta deben formar parte del origen de datos de SQL Server. Vea [Data Sources for DirectQuery Models](directquery-mode-ssas-tabular.md#bkmk_DataSources)para obtener más información.  
  
-   **Compatibilidad para columnas calculadas:** Las columnas calculadas no se admiten en los modelos DirectQuery. Sin embargo, puede crear medidas y KPI que actúen sobre conjuntos de datos. Para obtener más información, vea la sección que trata sobre la [validación](#bkmk_Validation) .  
  
-   **Uso limitado de funciones de DAX:** Algunas funciones DAX no se pueden usar en el modo DirectQuery, por lo que deberá sustituirlas por otras funciones o crear los valores con columnas derivadas en el origen de datos. El diseñador de modelos proporciona validación en tiempo de diseño para cualquier error que pueda surgir al crear fórmulas incompatibles con el modo DirectQuery. Vea las secciones siguientes para obtener más información: [Validación](#bkmk_Validation).  
  
-   **Compatibilidad de las fórmulas** En algunos casos conocidos, la misma fórmula puede devolver resultados distintos en un modelo en caché o híbrido en comparación con un modelo DirectQuery que use solamente el almacén de datos relacional. Estas diferencias son consecuencia de las diferencias semánticas entre el motor analítico en memoria xVelocity (VertiPaq) y SQL Server. Para obtener más información sobre estas diferencias, vea esta sección: [Compatibilidad de las fórmulas](#bkmk_FormulaCompat).  
  
-   **Seguridad:** Puede usar métodos diferentes para proteger los modelos en función de cómo se implementen estos. Los datos almacenados en caché para los modelos tabulares están protegidos mediante el modelo de seguridad de la instancia de Analysis Services. Los modelos de DirectQuery se pueden proteger utilizando roles, pero también puede utilizar la seguridad definida en el almacén de datos relacional. El modelo se puede configurar de modo que los usuarios que abran un informe basado en un modelo Solo DirectQuery puedan ver solo los datos que tengan autorizados en virtud de sus permisos de SQL Server. Vea esta sección para obtener más información: [Seguridad](#bkmk_Security).  
  
-   **Restricciones del cliente:** Cuando un modelo está en modo DirectQuery, solo se puede consultar con DAX. No se puede utilizar MDX para crear consultas. Esto significa que no podrá utilizar el cliente dinámico de Excel, porque Excel usa MDX.  
  
     Sin embargo, puede crear consultas en un modelo DirectQuery en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] si usa una consulta de tabla Dax como parte de una instrucción EXECUTE de XMLA. para obtener más información, vea [referencia de sintaxis de consulta Dax] (/Dax/Dax-Syntax-Reference
  
 Una vez haya resuelto todos los problemas de diseño y probado el modelo, estará listo para la implementación. En este momento, puede establecer el método preferido para responder a las consultas sobre el modelo. ¿Desea que los usuarios obtengan acceso a la memoria caché, o que utilicen siempre solamente el origen de datos relacional?  
  
 Si implementa el modelo en un *modo híbrido*, la memoria caché seguirá estando disponible y se podrá utilizar con las consultas. Un modo híbrido le ofrece muchas opciones:  
  
-   Si tanto la memoria caché como el origen de datos relacional están disponibles, puede establecer el método de conexión preferido, pero será el cliente el que en última instancia decida el origen que se utilizará, mediante la propiedad de cadena de conexión DirectQueryMode.  
  
-   También puede configurar particiones en la memoria caché de tal manera que la partición principal utilizada para el modo DirectQuery no se procese nunca y deba hacer siempre referencia al origen relacional. Hay muchas maneras de utilizar particiones para optimizar el diseño del modelo y la creación de informes. Para obtener más información, vea [particiones y el modo DirectQuery &#40;&#41;tabular de SSAS ](define-partitions-in-directquery-models-ssas-tabular.md).  
  
-   Una vez implementado el modelo, puede cambiar el método de conexión preferido. Por ejemplo, puede utilizar un modo híbrido para las pruebas, y cambiar el modelo a **Solo DirectQuery** únicamente después de probar exhaustivamente los informes o las consultas utilizadas por este. Para más información, vea [Establecer o cambiar el método de conexión preferido para DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).  
  
###  <a name="data-sources-for-directquery-models"></a><a name="bkmk_DataSources"></a>Orígenes de datos para los modelos DirectQuery  
 Tan pronto como cambie el entorno de diseño para habilitar el modo DirectQuery, se validarán los orígenes de datos de la base de datos del área de trabajo para garantizar que provienen de un único origen de datos de SQL Server. Los datos de otros orígenes, incluidos los datos de copiar y pegar, no se admiten en los modelos DirectQuery.  
  
 Si tiene previsto utilizar el modelo en el modo DirectQuery, debe asegurarse de que todos los datos que necesita para la creación de informes estén almacenados en la base de datos de SQL Server especificada. Si los datos que necesita para el modelado no están disponibles en ese origen, considere la posibilidad de utilizar Integration Services u otras herramientas de almacenamiento de datos para importar los datos en la base de datos de SQL Server que actúa como el origen de datos DirectQuery.  
  
###  <a name="validation-and-design-restrictions-for-directquery-mode"></a><a name="bkmk_Validation"></a>Restricciones de validación y diseño para el modo DirectQuery  
 Al crear un modelo para su uso en el modo DirectQuery, se deben cargar inicialmente parte de los datos en la memoria caché. Si los datos que va a usar es demasiado grande para caber en la memoria, puede usar la opción **vista previa & filtro** del Asistente para la importación de tablas para seleccionar un subconjunto de datos, o escribir un script SQL para obtener los datos que desea.  
  
> [!WARNING]  
>  Puesto que el modo DirectQuery no admite el uso de columnas calculadas, si hay alguna columna que desee combinar o en la que desee realizar otras operaciones, deberá planearlo por anticipado y crear la definición de columna como parte de la consulta o el script de importación de datos.  
  
 Para ver y resolver los errores de validación, abra la **Lista de errores** en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Los errores críticos que impiden el uso del modo DirectQuery se muestran en la pestaña **errores** . Debe corregir estos errores antes de cambiar al modo DirectQuery. Generalmente, los errores de validación más difíciles de resolver están relacionados con las fórmulas que no se admiten en el modo DirectQuery. Vea la sección [Compatibilidad de las fórmulas](#bkmk_FormulaCompat)para obtener información general sobre los errores relacionados con las fórmulas y las columnas calculadas.  
  
 La lista siguiente describe otras consideraciones que se han de tener en cuenta al crear un modelo para el acceso DirectQuery:  
  
-   En el modo *Solo DirectQuery* , los resultados del informe pueden variar en función del contexto de seguridad del usuario que esté viendo los resultados. Debe probar los modelos con distintas credenciales para asegurarse de que los usuarios consiguen los resultados previstos.  
  
-   Si configura un modelo para que funcione en el modo híbrido, lo que permitirá el uso de la memoria caché o de los datos de SQL Server, debe tener en cuenta la posibilidad de que los clientes que se conecten con cada origen vean resultados diferentes, en función del modo especificado en la cadena de conexión. Si necesita asegurarse de que los usuarios del informe vean solo los datos de SQL Server, debe borrar la memoria caché o cambiar el modelo a DirectQueryOnly.  
  
###  <a name="formula-compatibility-for-directquery-models"></a><a name="bkmk_FormulaCompat"></a>Compatibilidad de las fórmulas para los modelos DirectQuery  
 Algunos modelos pueden contener fórmulas que no se admiten en el modo DirectQuery; en estos casos, es necesario volver a diseñar el modelo para evitar los errores de validación. Entre las restricciones de las fórmulas que se admiten en el modo DirectQuery están las siguientes:  
  
-   Las columnas calculadas no se admiten en ningún modelo tabular que tenga habilitado el modo DirectQuery, ni siquiera en modelos híbridos. Si necesita columnas calculadas en un modelo, considere la posibilidad de convertirlas en columnas derivadas utilizando Transact-SQL en la definición de importación.  
  
-   Los modelos DirectQuery admiten el uso de fórmulas DAX en las medidas, que se convierten en operaciones basadas en conjuntos en el almacén de datos relacional. Se admiten todas las medidas creadas mediante medidas implícitas.  
  
-   No se admiten todas las funciones. Puesto que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] convierte todas las fórmulas DAX y las definiciones de medida en instrucciones SQL cuando se consulta un modelo DirectQuery, las fórmulas que contengan elementos que no se puedan convertir en Transact-SQL desencadenarán errores de validación en el modelo. Por ejemplo, las funciones de la inteligencia de tiempo no se admiten. Incluso las funciones admitidas pueden comportarse de forma diferente, como las funciones estadísticas. Para obtener una lista completa de los problemas de compatibilidad, vea [compatibilidad de las fórmulas en el modo DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md).  
  
-   Algunas fórmulas del modelo pueden validarse al cambiar este al modo DirectQuery, pero devolver resultados diferentes cuando se ejecutan en la memoria caché en comparación con el almacén de datos relacional. Esto es debido a que los cálculos en la memoria caché utilizan la semántica del motor analítico en memoria xVelocity (VertiPaq), que contiene muchas características cuya finalidad es emular el comportamiento de Excel, mientras que las consultas en los datos almacenados en el almacén de datos relacional utilizan necesariamente la semántica de SQL Server. Para obtener una lista de las funciones DAX que pueden devolver resultados diferentes cuando el modelo se implementa en tiempo real, vea [compatibilidad de las fórmulas en el modo DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md).  
  
###  <a name="connecting-to-directquery-models"></a><a name="bkmk_Connecting"></a>Conectar con los modelos DirectQuery  
 Los clientes que utilicen MDX como lenguaje de consultas no podrán conectarse a los modelos que utilizan el modo DirectQuery. Por ejemplo, si intenta crear una consulta MDX en un modelo DirectQuery, aparecerá un error que indica que no se puede encontrar el cubo, o que este no se ha procesado. Puede crear consultas en los modelos DirectQuery utilizando [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], fórmulas DAX o consultas XMLA. Para obtener más información sobre cómo realizar consultas ad hoc en modelos tabulares, vea [Tabular Model Data Access](tabular-model-data-access.md).  
  
 Si va a utilizar un modelo híbrido, puede especificar si los usuarios se conectarán a la memoria caché o utilizarán datos DirectQuery especificando la propiedad de cadena de conexión, DirectQueryMode.  
  
###  <a name="security-in-directquery-mode"></a><a name="bkmk_Security"></a>Seguridad en el modo DirectQuery  
 Los permisos que se utilizan para recuperar los datos de origen se deben especificar durante el proceso de creación del modelo. A menudo, serán sus propias credenciales o una cuenta que se use para el desarrollo. Sin embargo, cuando se cambia el modelo al modo DirectQuery, el contexto de seguridad es más complejo:  
  
-   Considere si los usuarios tienen el nivel de acceso necesario a los datos del almacén de datos relacional.  
  
-   Los usuarios que ven el mismo modelo o informe pueden ver datos diferentes, en función del contexto de seguridad del usuario.  
  
-   Si se ha conservado la memoria caché de modelos, dicha memoria debe protegerse con los (roles) de modelo de seguridad de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Es posible que la memoria caché contenga datos que puede ver el diseñador de modelos pero no otros usuarios. Los diseñadores de modelos y de informes deben borrar la memoria caché o proteger estos datos controlando el acceso a ellos mediante roles.  
  
-   Un modelo que responda a las consultas de la memoria caché no puede suplantar al usuario actual al conectarse al origen de datos. Si desea suplantar al usuario actual al conectarse al origen de datos, debe utilizar el modo DirectQuery.  
  
-   Si su modelo de informe requiere funciones de seguridad, dispone de dos opciones: utilizar los roles de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o establecer permisos para el origen de datos en el nivel de fila. La seguridad en el origen de datos relacional se utiliza para controlar el acceso a las tablas, y no se admite la seguridad en el nivel de columna. Por lo tanto, si los usuarios de una región no tienen permiso para ver las cifras de ventas de otras regiones, un informe que incluya una medida basada en la tabla de ventas devolverá espacios en blanco o un error.  
  
 La propiedad de los valores de suplantación especifica las credenciales utilizadas al conectarse a un modelo con DirectQuery, ya sea para un modelo Solo DirectQuery o para un modelo híbrido que responda a consultas mediante DirectQuery. La propiedad tiene los siguientes valores:  
  
 **Valor predeterminado**  
 Utiliza las credenciales especificadas en el asistente para la importación para conectarse al origen de datos. Puede ser un usuario específico de Windows o la cuenta de servicio.  
  
 `ImpersonateCurrentUser`  
 Usa las credenciales de Windows del usuario actual para conectarse al origen de datos.  
  
 Para obtener información sobre cómo establecer estas propiedades, vea [escenarios de implementación de DirectQuery &#40;&#41;tabulares de SSAS ](../directquery-deployment-scenarios-ssas-tabular.md).  
  
##  <a name="directquery-properties"></a><a name="bkmk_PropertyList"></a>Propiedades de DirectQuery  
 La tabla siguiente enumera las propiedades que se pueden establecer en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]para habilitar DirectQuery y controlar el origen de los datos utilizado para las consultas en el modelo.  
  
|Nombre de propiedad|Descripción|  
|-------------------|-----------------|  
|**Propiedad DirectQueryMode**|Esta propiedad habilita el uso del modo DirectQuery en el diseñador de modelos. Se debe establecer en `On` para cambiar cualquiera de las otras propiedades de DirectQuery.<br /><br /> Para obtener más información, vea [Habilitar el modo de diseño de DirectQuery &#40;&#41;tabular de SSAS ](enable-directquery-mode-in-ssdt.md).|  
|**Propiedad QueryMode**|Esta propiedad especifica el método de consulta predeterminado para un modelo DirectQuery. Se establece en el diseñador de modelos al implementar el modelo, pero se puede invalidar más adelante. La propiedad tiene estos valores:<br /><br /> **DirectQuery** : este valor especifica que todas las consultas al modelo deben utilizar solo el origen de datos relacional.<br /><br /> **DirectQuery con In-Memory** : este valor especifica que, de forma predeterminada, las consultas se deben responder con el origen relacional, a menos que se especifique lo contrario en la cadena de conexión desde el cliente.<br /><br /> **In-Memory** : este valor especifica que las consultas tienen que responderse únicamente con la caché.<br /><br /> **In-Memory con DirectQuery** : este valor especifica, de forma predeterminada, que las consultas se deben responder mediante caché, a menos que se especifique lo contrario en la cadena de conexión de cliente.<br /><br /> <br /><br /> Para más información, vea [Establecer o cambiar el método de conexión preferido para DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).|  
|**Propiedad DirectQueryMode**|Una vez implementado el modelo, es posible cambiar el origen de datos preferido de la consulta para un modelo DirectQuery modificando esta propiedad en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].<br /><br /> Al igual que la propiedad anterior, esta propiedad especifica el origen de datos predeterminado para el modelo, y tiene estos valores:<br /><br /> **InMemory**: Las consultas solo pueden usar la memoria caché.<br /><br /> **DirectQuerywithInMemory**: Las consultas usan el origen de datos relacional de forma predeterminada, a menos que se especifique lo contrario en la cadena de conexión desde el cliente.<br /><br /> **InMemorywithDirectQuery**: Las consultas usan la memoria caché de forma predeterminada, a menos que se especifique lo contrario en la cadena de conexión desde el cliente.<br /><br /> (**DirectQuery**: las consultas solo usan el origen de datos relacional.<br /><br /> <br /><br /> Para más información, vea [Establecer o cambiar el método de conexión preferido para DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md).|  
|**Propiedad Configuración de suplantación**|Esta propiedad define las credenciales que se utilizan para conectarse con el origen de datos de SQL Server en el momento de la consulta. Puede establecer esta propiedad en el diseñador de modelos y cambiar su valor más adelante, una vez implementado el modelo.<br /><br /> Tenga en cuenta que estas credenciales solo se utilizan para responder a las consultas en el almacén de datos relacional; no son las mismas que se usan para procesar la memoria caché de un modelo híbrido.<br /><br /> No se puede utilizar la suplantación si el modelo solo se usa en la memoria. El valor `ImpersonateCurrentUser` no es válido a menos que el modelo utilice el modo DirectQuery.|  
  
 Además, si el modelo incluye particiones, deberá elegir una que actuará como origen para las consultas en el modo DirectQuery. Para obtener más información, vea [particiones y el modo DirectQuery &#40;&#41;tabular de SSAS ](define-partitions-in-directquery-models-ssas-tabular.md).  
  
##  <a name="related-topics-and-tasks"></a><a name="bkmk_related_tasks"></a>Temas y tareas relacionados  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Particiones y modo DirectQuery &#40;&#41;tabular de SSAS](define-partitions-in-directquery-models-ssas-tabular.md)|Describe cómo las particiones se utilizan en los modelos configurados para el modo DirectQuery.|  
|[Compatibilidad de las fórmulas DAX en el modo DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|Describe las restricciones y los requisitos de compatibilidad en las fórmulas que se pueden usar en modelos configurados para el modo DirectQuery.|  
|[Habilitar el modo de diseño DirectQuery &#40;SSAS tabular&#41;](enable-directquery-mode-in-ssdt.md)|Describe cómo se puede cambiar el entorno en tiempo de diseño para que admita el uso del modo DirectQuery.|  
|[Cambiar la partición de DirectQuery &#40;la&#41;tabular de SSAS](../change-the-directquery-partition-ssas-tabular.md)|Describe cómo cambiar la partición de DirectQuery.|  
|[Establecer o cambiar el método de conexión preferido para DirectQuery](../set-or-change-the-preferred-connection-method-for-directquery.md)|Describe cómo establecer o cambiar el método de conexión de los modelos configurados para DirectQuery.|  
|[Escenarios de implementación de DirectQuery &#40;&#41;tabular de SSAS](../directquery-deployment-scenarios-ssas-tabular.md)|Describe los escenarios de implementación de DirectQuery.|  
|[Configurar el acceso In-Memory o DirectQuery para una base de datos modelo tabular](enable-directquery-mode-in-ssms.md)|Entender las configuraciones de DirectQuery|  
|[Borrar las memorias caché de Analysis Services](../instances/clear-the-analysis-services-caches.md)|Borrar la memoria caché del modelo tabular|  
  
## <a name="see-also"></a>Consulte también  
 [Particiones &#40;&#41;tabular de SSAS](partitions-ssas-tabular.md)   
 [Proyectos de modelos tabulares &#40;&#41;tabular de SSAS](tabular-model-projects-ssas-tabular.md)   
 [Analizar en Excel &#40;SSAS tabular&#41;](analyze-in-excel-ssas-tabular.md)  
