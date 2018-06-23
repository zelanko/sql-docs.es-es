---
title: Habilitar y deshabilitar el espacio aislado de RDL | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d5619e9f-ec5b-4376-9b34-1f74de6fade7
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 0fefbebb9c56df87c83bb3b41ee508550a5f2113
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200076"
---
# <a name="enable-and-disable-rdl-sandboxing"></a>Habilitar y deshabilitar el espacio seguro para RDL
  La característica de espacio aislado del lenguaje RDL (Report Definition Language) permite detectar y restringir el uso de tipos específicos de uso de recursos por parte de inquilinos individuales en un entorno donde varios inquilinos usan una única granja web de servidores de informes. Un ejemplo de esto es un escenario de servicios de hospedaje en el que podría mantener una única granja web de servidores de informes que utilicen varios inquilinos, y quizás compañías diferentes. Como administrador del servidor de informes, puede habilitar esta característica para alcanzar los siguientes objetivos:  
  
-   Restringir los tamaños de recursos externos. Entre los recursos externos se incluyen imágenes, archivos .xslt y datos de mapas.  
  
-   En el tiempo de publicación del informe, limitar los tipos y los miembros que se usan en el texto de expresión.  
  
-   En el tiempo de procesamiento del informe, limitar la longitud del texto y el texto del valor de devolución de las expresiones.  
  
 Cuando se habilita el espacio aislado de RDL, se deshabilitan las siguientes características:  
  
-   Código personalizado en el elemento **\<Code>** de una definición de informe.  
  
-   Modo de compatibilidad con versiones anteriores de RDL para los elementos de informe personalizados de [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] .  
  
-   Parámetros con nombre en expresiones.  
  
 En este tema se describe cada elemento en el <`RDLSandboxing`> elemento en el archivo RSReportServer.Config. Para más información sobre cómo modificar este archivo, vea [Modificar un archivo de configuración de Reporting Services &#40;RSreportserver.config&#41;](report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md). Un registro de seguimiento del servidor guarda la actividad relacionada con la característica de espacio aislado de RDL. Para obtener más información acerca de los registros de seguimiento, vea [Report Server Service Trace Log](report-server/report-server-service-trace-log.md).  
  
## <a name="example-configuration"></a>Ejemplo de configuración  
 En el ejemplo siguiente se muestra la configuración y los valores de ejemplo para el <`RDLSandboxing`> elemento en el archivo RSReportServer.Config.  
  
```  
<RDLSandboxing>  
   <MaxExpressionLength>5000</MaxExpressionLength>  
   <MaxResourceSize>5000</MaxResourceSize>  
   <MaxStringResultLength>3000</MaxStringResultLength>  
   <MaxArrayResultLength>250</MaxArrayResultLength>  
   <Types>  
      <Allow Namespace=”System.Drawing” AllowNew=”True”>Bitmap</Allow>  
      <Allow Namespace=”TypeConverters.Custom” AllowNew=”True”>*</Allow>  
   </Types>  
   <Members>  
      <Deny>Format</Deny>  
      <Deny>StrDup</Deny>  
   </Members>  
</RDLSandboxing>  
```  
  
## <a name="configuration-settings"></a>Parámetros de configuración  
 La siguiente tabla proporciona información acerca de los parámetros de configuración. Los parámetros se presentan en el orden en que aparecen en el archivo de configuración.  
  
|Configuración|Descripción|  
|-------------|-----------------|  
|**MaxExpressionLength**|Número máximo de caracteres permitido en expresiones RDL.<br /><br /> Valor predeterminado: 1000|  
|**MaxResourceSize**|Número máximo de KB permitido para un recurso externo.<br /><br /> Valor predeterminado: 100|  
|**MaxStringResultLength**|Número máximo de caracteres permitido en un valor de devolución para una expresión RDL.<br /><br /> Valor predeterminado: 1000|  
|**MaxArrayResultLength**|Número máximo de elementos permitido en un valor de devolución de matriz para una expresión RDL.<br /><br /> Valor predeterminado: 100|  
|**Tipos**|Lista de los miembros que se permitirán en las expresiones RDL.|  
|**Allow**|Tipo o conjunto de tipos que se permitirán en las expresiones RDL.|  
|**Espacio de nombres**|Atributo de **Allow** que es el espacio de nombres que contiene uno o varios tipos que se aplican a Value. Esta propiedad no distingue entre mayúsculas y minúsculas.|  
|`AllowNew`|Atributo booleano de **Allow** que controla si se permite que las nuevas instancias del tipo se creen en expresiones RDL o en un elemento **\<Class>** de RDL.<br /><br /> Nota: Cuando `RDLSandboxing` está habilitada, no se puede crear nuevas matrices en expresiones RDL, independientemente de la configuración de `AllowNew`.|  
|**Value**|Valor de **Allow** que es el nombre del tipo que se permitirá en las expresiones RDL. El valor **\*** indica que se permiten todos los tipos del espacio de nombres. Esta propiedad no distingue entre mayúsculas y minúsculas.|  
|**Miembros**|Para la lista de tipos que se incluyen en el elemento **\<Types>**, la lista de nombres de miembro que no se permiten en las expresiones RDL.|  
|**Denegar**|Nombre de un miembro que no se permite en expresiones RDL. Esta propiedad no distingue entre mayúsculas y minúsculas.<br /><br /> Nota: Cuando se especifica **Deny** para un miembro, no se permite ningún miembro con este nombre para todos los tipos.|  
  
## <a name="working-with-expressions-when-rdl-sandboxing-is-enabled"></a>Trabajar con expresiones cuando se habilita el espacio aislado de RDL  
 Puede modificar la característica de espacio aislado de RDL para administrar los recursos que usa una explorador de las siguientes formas:  
  
-   Restringir el número de caracteres que se usa para una expresión.  
  
-   Restringir el tamaño del resultado devuelto por una expresión.  
  
-   Permitir una lista específica de tipos que se pueden usar en una expresión.  
  
-   Restringir la lista de miembros por nombre para la lista de tipos permitidos que se pueden usar en una expresión.  
  
-   La característica de espacio aislado de RDL permite crear una lista de tipos aprobados y una lista de miembros denegados. La lista de tipos aprobados se denomina lista de permitidos. La lista de miembros denegados se denomina lista de bloqueados.  
  
> [!NOTE]  
>  En la definición de informe, un equipo no puede conocer el tipo de cada instancia de una referencia de expresión. Al agregar un miembro a la lista de bloqueados, se están denegando todos los miembros de ese nombre en todos los tipos de la lista de permitidos.  
  
 Los resultados de la expresión RDL se comprueban en tiempo de ejecución. Las expresiones RDL se comprueban en la definición de informe cuando se publica el informe. Supervise el registro de seguimiento del servidor de informes por si se han producido infracciones. Para obtener más información, consulte [Report Server Service Trace Log](report-server/report-server-service-trace-log.md).  
  
### <a name="working-with-types"></a>Trabajar con tipos  
 Al agregar un tipo a la lista de permitidos, se controlan los siguientes puntos de entrada para obtener acceso a las expresiones RDL:  
  
-   Miembros estáticos de un tipo.  
  
-   El [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] `New` método.  
  
-   El elemento **\<Classes>** en la definición del informe.  
  
-   Miembros que ha agregado a la lista de bloqueados para un tipo de la lista de permitidos.  
  
 La lista de permitidos no controla los siguientes puntos de entrada:  
  
-   Conjuntos de datos de informe. Los campos de los conjuntos de datos de informe que se devuelven de las consultas pueden contener cualquier tipo RDL válido.  
  
-   Parámetros de informe. Los valores de parámetro proporcionados por el usuario pueden contener cualquier tipo RDL válido.  
  
-   Miembros de un tipo habilitado que no están en la lista de bloqueados. De forma predeterminada, todos los miembros de todos los tipos de la lista de permitidos están habilitados. Al agregar un nombre de miembro a la lista de bloqueados, se están denegando todos los miembros con ese nombre en todos los tipos que están en la lista de permitidos.  
  
 Para habilitar un miembro de un tipo pero denegar un miembro con el mismo nombre de otro tipo, debe realizar las siguientes operaciones:  
  
-   Agregar un elemento **\<Deny>** para el nombre de miembro.  
  
-   Crear un miembro de proxy con otro nombre en una clase de un ensamblado personalizado para el miembro que desea habilitar.  
  
-   Agregar la nueva clase a la lista de permitidos.  
  
 Para agregar [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] funciones de .NET Framework a la lista de permitidos, agregue los tipos correspondientes del espacio de nombres Microsoft.VisualBasic a la lista de permitidos.  
  
 Para agregar palabras clave de tipo de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework a la lista de permitidos, agregue el tipo CLR correspondiente a la lista de permitidos. Por ejemplo, para usar el [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] palabra clave de .NET Framework `Integer`, agregue el siguiente fragmento XML para el  **\<RDLSandboxing >** elemento:  
  
```  
<Allow Namespace="System">Int32</Allow>  
```  
  
 Para agregar un tipo genérico o que admite valores NULL de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework a la lista de permitidos, debe realizar las siguientes operaciones:  
  
-   Crear un tipo de proxy para el tipo genérico o que admite valores NULL de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework.  
  
-   Agregar el tipo de proxy a la lista de permitidos.  
  
 Al agregar un tipo de un ensamblado personalizado a la lista de permitidos no se concede permiso de ejecución de forma explícita en el ensamblado. Debe modificar de forma específica el archivo de seguridad de acceso del código y proporcionar el permiso de ejecución en el ensamblado. Para más información, consulte [Code Access Security in Reporting Services](extensions/secure-development/code-access-security-in-reporting-services.md).  
  
#### <a name="maintaining-the-deny-list-of-members"></a>Mantener la \<denegar > lista de miembros  
 Al agregar un nuevo tipo a la lista de permitidos, use la siguiente lista para determinar cuándo tendrá que actualizar la lista de miembros bloqueados:  
  
-   Al actualizar un ensamblado personalizado con una versión que introduce nuevos tipos.  
  
-   Al agregar los miembros a los tipos de la lista de permitidos.  
  
-   Al actualizar el [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] en el servidor de informes.  
  
-   Al actualizar el servidor de informes a una versión posterior de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   Al actualizar un servidor de informes para administrar un esquema RDL posterior, porque se pueden haber agregado nuevos miembros a los tipos RDL.  
  
### <a name="working-with-operators-and-new"></a>Trabajar con operadores y New  
 De forma predeterminada, los operadores del lenguaje [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework siempre están permitidos, excepto para `New`. El `New` operador se controla mediante la `AllowNew` del atributo en el  **\<permitir >** elemento. Otros operadores de lenguaje, como el operador de descriptor de acceso de colección predeterminada `!` y [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] .NET Framework como macros de conversión `CInt`, siempre están permitidos.  
  
 No se admite la adición de operadores a la lista de bloqueados, incluidos los operadores personalizados. Para excluir los operadores de un tipo, debe realizar las siguientes operaciones:  
  
-   Crear un tipo de proxy que no implemente los operadores que desee excluir.  
  
-   Agregar el tipo de proxy a la lista de permitidos.  
  
 Para crear una nueva matriz en una expresión RDL, cree la matriz en un método de una clase que haya definido y agregue dicha clase a la lista de permitidos.  
  
 Para crear una nueva matriz en una expresión RDL, debe realizar las siguientes operaciones:  
  
-   Definir una nueva clase y crear la matriz en un método de dicha clase.  
  
-   Agregar la clase a la lista de permitidos.  
  
## <a name="see-also"></a>Vea también  
 [Archivo de configuración RSReportServer](report-server/rsreportserver-config-configuration-file.md)   
 [Registro de seguimiento del servicio del servidor de informes](report-server/report-server-service-trace-log.md)  
  
  