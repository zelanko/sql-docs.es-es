---
title: Tipo de conexión de lista de SharePoint (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2c4adf2f-e9c4-4fae-bd3c-97fe64436caf
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 129fabab52b2e7b7e59cf832d21e25972cb9b07a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260401"
---
# <a name="sharepoint-list-connection-type-ssrs"></a>Tipo de conexión de lista de SharePoint (SSRS)
  Para incluir los datos de una lista de Microsoft SharePoint en el informe, debe agregar o crear un conjunto de datos basado en un origen de datos de informe de tipo de lista de Microsoft SharePoint. Este es un tipo de origen de datos integrado que se basa en la extensión de datos de lista de SharePoint de Microsoft SQL Server Reporting Services. Utilice este tipo de origen de datos para conectarse a, y recuperar datos de lista de, los sitios de [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], [!INCLUDE[SPS2010](../../includes/sps2010-md.md)], [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0 y [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007.  
  
 Utilice la información de este tema para crear un origen de datos. Para obtener instrucciones detalladas, consulte [agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadena de conexión  
 La cadena de conexión a una lista de SharePoint es la dirección URL al sitio o subsitio de SharePoint; por ejemplo, `http://MySharePointWeb/MySharePointSite` o `http://MySharePointWeb/MySharePointSite/Subsite`.  
  
 El diseñador de consultas muestra automáticamente las listas de SharePoint para las que el usuario tiene los permisos necesarios para obtener acceso.  
  
 Para más información sobre ejemplos de cadenas de conexión, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenciales  
 Se necesitan credenciales para ejecutar consultas y obtener una vista previa del informe localmente y desde el servidor de informes. Después de publicar el informe, es posible que necesite cambiar las credenciales para el origen de datos de tal forma que, cuando el informe se ejecute en el servidor de informes, los permisos para recuperar los datos sean válidos. Los tipos de credenciales que se pueden utilizar con esta extensión de datos dependen de la configuración de la tecnología de SharePoint para la lista de SharePoint que se esté utilizando como origen de datos.  
  
 En las tablas siguientes se describe el comportamiento de recuperación de credenciales de la extensión de lista de SharePoint cuando se conecta a una lista de SharePoint de una granja local y a una lista remota de SharePoint.  
  
 La**tabla 1** es para los informes implementados en un sitio heredado de Windows SharePoint. Un sitio heredado de Windows solo admite Kerberos, NTLM y Autenticación basada en formularios (FBA). La**tabla 2** es para los informes implementados en un sitio de SharePoint basado en notificaciones.  
  
 **tabla 1**  
  
||Credenciales admitidas|Autenticación de Windows de modo clásico|<sup>3</sup> autenticación mediante formularios|  
|-|---------------------------|-----------------------------------------|----------------------------------------|  
|Lista de SharePoint de granja local|Autenticación de Windows (integrada) o Token de usuario de SharePoint|Sí|Sí|  
||Almacenada, pedir, ninguna (con credenciales de Windows<sup>1</sup>)|Sí|no|  
|Lista remota de SharePoint|Autenticación de Windows (integrada) o Token de usuario de SharePoint|Sí|No<sup>2</sup>|  
||Almacenada, pedir, ninguna (con credenciales de Windows<sup>1</sup>)|Sí|No<sup>2</sup>|  
  
 **tabla 2**  
  
||Credenciales admitidas|Autenticación de Windows de modo clásico|<sup>3</sup> autenticación mediante formularios|  
|-|---------------------------|-----------------------------------------|----------------------------------------|  
|Lista de SharePoint de granja local|Autenticación de Windows (integrada) o Token de usuario de SharePoint|Sí|Sí|  
||Almacenada, pedir, ninguna (con credenciales de Windows<sup>1</sup>)|no|no|  
|Lista remota de SharePoint|Autenticación de Windows (integrada) o Token de usuario de SharePoint|Sí|No<sup>2</sup>|  
||Almacenada, pedir, ninguna (con credenciales de Windows<sup>1</sup>)|no|No<sup>2</sup>|  
  
 <sup>1</sup> almacenadas y símbolo del sistema con credenciales que no son Windows no se admite.  
  
 <sup>2</sup> autenticación basada en formularios y la autenticación de notificaciones no se admiten para las listas de SharePoint remoto.  
  
 <sup>3</sup> proveedores de autenticación mencionados de autenticación de Windows, autenticación basada en formularios (FBA), tokens de Secure Application Markup Language (SAML), otros proveedores de identidad o una combinación de más de uno de los pasos anteriores.  
  
 **Autenticación de Windows**  
 Esta opción no se admite en el caso de una tecnología de SharePoint que esté configurada para trabajar con un servidor de informes en el modo de cuenta de confianza. Esto solo se aplica a las versiones anteriores a SQL Server 2012 Reporting Services.  
  
 En el caso de una tecnología de SharePoint que esté configurada para trabajar con un servidor de informes en el modo integrado de Windows, esta opción se aplica tanto al usuario de Windows actual como al usuario de SharePoint actual.  
  
 En el caso de una tecnología de SharePoint configurada para funcionar sin un servidor de informes (modo local), esta opción no se admite. Para obtener más información sobre el modo local, vea [Informes en modo local frente al modo conectado en el Visor de informes &#40;Reporting Services en modo de SharePoint&#41;](../local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md).  
  
 **No se necesitan credenciales (No usar credenciales):**  
 Para usar esta opción, la cuenta de ejecución desatendida debe estar configurada en el servidor de informes. Para obtener más información, vea [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 Para obtener información sobre la compatibilidad con la autenticación basada en notificaciones en la pila de Microsoft BI, vea [Usar autenticación basada en notificaciones en la pila de Microsoft BI](http://social.technet.microsoft.com/wiki/contents/articles/15274.using-claims-authentication-across-the-microsoft-bi-stack.aspx).  
  
 Para obtener más información, consulte [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md), [especificar credenciales en Generador de informes](../specify-credentials-in-report-builder.md), y [Data Sources Supported by Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
##  <a name="Query"></a> Consultas  
 Para diseñar una consulta, cree un nuevo conjunto de datos basado en el origen de datos y, a continuación, abra el diseñador de consultas asociado. Para obtener más información, vea [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
 El diseñador gráfico de consultas de lista de SharePoint muestra cuatro paneles:  
  
 **Listas de SharePoint**  Muestra una lista con todas las listas de SharePoint del sitio para este origen de datos. Seleccione una lista y, a continuación, seleccione los campos que desea en su consulta. Los nombres de los campos de este panel son solo nombres descriptivos de SharePoint, también conocidos como nombres para mostrar. Mantenga el mouse sobre un elemento para que se muestren las propiedades siguientes en la información sobre herramientas:  
  
-   **Nombre** Nombre único del campo.  
  
-   **Identificador** Identificador único del campo.  
  
-   **Tipo de campo** Tipo de datos del campo.  
  
-   **Oculto** Determina si el campo se muestra en la vista de lista de SharePoint.  
  
 No se admite la selección de campos de varias listas. Puede crear un conjunto de datos para cada lista y seleccionar campos de cada conjunto de datos. Si las listas tienen un campo común, puede utilizar la función de búsqueda en una región de datos de Tablix enlazada a un conjunto de datos para recuperar un valor del otro conjunto de datos que no está enlazado a la región de datos. Para obtener más información, vea [Función Lookup &#40;Generador de informes y SSRS&#41;](../report-design/report-builder-functions-lookup-function.md).  
  
-   **Campos seleccionados**  Muestra los campos que se han seleccionado. Los nombres de campo de este panel son solo nombres descriptivos especificados por un usuario de SharePoint. Al cerrar el diseñador de consultas, estos nombres se ven en la colección de campos de conjunto de datos en el panel Datos de informe. La relación entre los nombres únicos y los nombres descriptivos está disponible en la página [Propiedades del conjunto de datos (cuadro de diálogo), Campos &#40;Generador de informes&#41;](../dataset-properties-dialog-box-fields-report-builder.md).  
  
-   **Filtros aplicados**  Limita los datos que se devuelven desde la lista de SharePoint, antes de que los datos se devuelvan al informe. Seleccione el nombre de campo, el operador y el valor que se deben usar para limitar los datos que se recuperan de la lista. Los operadores varían en función del tipo de datos del valor que se seleccione.  
  
     No se puede cambiar el criterio de ordenación ni especificar grupos en el diseñador gráfico de consultas. Para hacerlo, se deben configurar expresiones de ordenación en el conjunto de datos del informe y expresiones de grupo en las regiones de datos del informe. No se admiten parámetros de consulta. Para filtrar los datos del informe, use filtros de informe o parámetros de informe creados por usted. Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) y [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
-   **Resultados de consulta**  Muestra filas de ejemplo que se devuelven cuando se ejecuta la consulta. Si los valores de lista de SharePoint cambian con frecuencia en el sitio de SharePoint, los valores que se ven en el panel de resultados de la consulta podrían diferir de los valores que se ven en el informe.  
  
-   **Campos seleccionados**  Muestra los campos que se han seleccionado. Los nombres de campo de este panel son solo nombres descriptivos especificados por un usuario de SharePoint. Al cerrar el diseñador de consultas, estos nombres se ven en la colección de campos de conjunto de datos en el panel Datos de informe. La relación entre los nombres únicos y los nombres descriptivos está disponible en la página [Propiedades del conjunto de datos (cuadro de diálogo), Campos &#40;Generador de informes&#41;](../dataset-properties-dialog-box-fields-report-builder.md).  
  
-   **Filtros aplicados**  Limita los datos que se devuelven desde la lista de SharePoint, antes de que los datos se devuelvan al informe. Seleccione el nombre de campo, el operador y el valor que se deben usar para limitar los datos que se recuperan de la lista. Los operadores varían en función del tipo de datos del valor que se seleccione.  
  
     No se puede cambiar el criterio de ordenación ni especificar grupos en el diseñador gráfico de consultas. Para hacerlo, se deben configurar expresiones de ordenación en el conjunto de datos del informe y expresiones de grupo en las regiones de datos del informe. No se admiten parámetros de consulta. Para filtrar los datos del informe, use filtros de informe o parámetros de informe creados por usted. Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) y [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
-   **Resultados de consulta**  Muestra filas de ejemplo que se devuelven cuando se ejecuta la consulta. Si los valores de lista de SharePoint cambian con frecuencia en el sitio de SharePoint, los valores que se ven en el panel de resultados de la consulta podrían diferir de los valores que se ven en el informe.  
  
 Para obtener más información, vea [Diseñador de consultas de lista de SharePoint &#40;Generador de informes&#41;](sharepoint-list-query-designer-report-builder.md).  
  
### <a name="query-text"></a>Texto de consulta  
 Para ver la consulta generada por el diseñador gráfico de consultas, cambie al diseñador de consultas basado en texto. En esta vista, puede ver el XML creado por el diseñador gráfico de consultas. El XML incluye elementos para el nombre de la lista, la colección de campos y el filtro.  
  
#### <a name="example-1-specified-fields-for-a-list"></a>Ejemplo 1. Campos especificados para una lista  
 En el siguiente ejemplo se muestra una consulta de SharePoint con el formato correcto:  
  
```  
<RSSharePointList>  
<listName>MyList</listName>  
<viewFields>  
  <FieldRef Name="Field1"/>  
  <FieldRef Name="Field4"/>  
</viewFields>  
<Query>  
  <Where>  
    <And>  
      <Gt>  
        <FieldRef Name="Field1"/>  
        <Value Type="Integer">1</Value>  
      </Gt>  
      <IsNotNull>  
        <FieldRef Name="Field2"/>  
        <Value Type="string"/>  
      </IsNotNull>   
    </And>  
  </Where>  
</Query>  
</RSSharePointList>  
```  
  
 Puede modificar esta vista de la consulta, siempre que siga siendo texto XML con el formato correcto.  
  
#### <a name="example-2-all-fields-for-a-list"></a>Ejemplo 2. Todos los campos para una lista  
 También puede especificar solo el nombre de una lista y se devuelven todos los campos, incluidos los campos ocultos. En el siguiente ejemplo se recuperan todos los campos de una lista denominada Tareas:  
  
```  
<RSSharePointList>  
<listName>Tasks</listName>  
</RSSharePointList>  
```  
  
 Todos los campos de la lista Tareas se devuelven en los resultados de la consulta.  
  
##  <a name="Parameters"></a> Parámetros  
 Esta extensión de datos no admite parámetros.  
  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 Esta sección contiene instrucciones paso a paso para trabajar con conexiones de datos, orígenes de datos y conjuntos de datos.  
  
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Agregar un filtro a un conjunto de datos &#40;Generador de informes y SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Secciones relacionadas  
 Estas secciones de la documentación proporcionan información conceptual detallada sobre los datos de informe, así como información de procedimientos acerca de cómo definir, personalizar y usar las partes de un informe que están relacionadas con datos.  
  
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)  
 Proporciona información general sobre cómo obtener acceso a los datos del informe.  
  
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Proporciona información sobre las conexiones de datos y los orígenes de datos.  
  
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Proporciona información sobre conjuntos de datos compartidos e incrustados.  
  
 [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Proporciona información sobre la colección de campos de conjunto de datos que genera la consulta.  
  
 [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) en la documentación relativa a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](http://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Proporciona información detallada sobre la compatibilidad de versiones y plataformas para cada extensión de datos.  
  
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
