---
title: "Descripción de las directivas de seguridad | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- code groups [Reporting Services]
- code access security [Reporting Services], security policies
- Execution permission set
- custom assemblies [Reporting Services], security
- permission sets [Reporting Services]
- expressions [Reporting Services], security
- evidence [Reporting Services]
- FullTrust permission set
- security policies [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: a9bf043a-139a-4929-9a58-244815323df0
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4cb028a3034ddd4dbee5ee3d1b10f696bbe995f3
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="understanding-security-policies"></a>Descripción de las directivas de seguridad
  Cualquier código ejecutado por un servidor de informes debe formar parte de una directiva de seguridad de acceso del código concreta. Estas directivas de seguridad constan de grupos de código que asignan evidencias a un conjunto de conjuntos de permisos con nombre. Con frecuencia, los grupos de código están asociados a un conjunto de permisos con nombre que especifica los permisos que puede tener el código de ese grupo. El motor en tiempo de ejecución usa las evidencias proporcionadas por un host de confianza o por el cargador para determinar a qué grupos de código pertenece el código y, por tanto, qué permisos se deben conceder al código. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]cumple esta arquitectura de directiva de seguridad de acuerdo con la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] common language runtime (CLR). En las secciones siguientes se describen los distintos tipos de código de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y las reglas de directivas asociadas a los mismos.  
  
## <a name="report-server-assemblies"></a>Ensamblados del servidor de informes  
 Los ensamblados del servidor de informes son aquellos que contienen código que forma parte del producto [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] se escribe mediante ensamblados de código administrado; todos estos ensamblados tienen nombres seguros (es decir, están firmados digitalmente). Los grupos de código de estos ensamblados se definen mediante la **StrongNameMembershipCondition**, que proporciona evidencias basadas en información de clave pública de nombre seguro del ensamblado. El grupo de código se le concede la **FullTrust** conjunto de permisos.  
  
## <a name="report-server-extensions-rendering-data-delivery-and-security"></a>Extensiones del servidor de informes (Representación, Datos, Entrega y Seguridad)  
 Las extensiones del servidor de informes son extensiones de seguridad, representación, entrega y datos personalizados que crean los usuarios para extender la funcionalidad de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Debe conceder **FullTrust** a estas extensiones o código de ensamblado en los archivos de configuración de directiva asociada a la [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] está ampliando el componente. Las extensiones incluidas como parte de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] están firmados con la clave pública del servidor de informes y recibir el **FullTrust** conjunto de permisos.  
  
> [!IMPORTANT]  
>  Debe modificar el [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] archivos de configuración de directiva para permitir que **FullTrust** para las extensiones de terceros. Si no se agrega un grupo de código con **FullTrust** para sus extensiones personalizadas, no se puede usar el servidor de informes.  
  
 Para obtener más información acerca de los archivos de configuración de directiva [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], consulte [Using Reporting Services Security Policy Files](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).  
  
## <a name="expressions-used-in-reports"></a>Expresiones usadas en informes  
 Expresiones de informe son expresiones de código insertado o métodos definidos por el usuario dentro de la **código** elemento de un archivo de lenguaje de definición de informe. Hay un grupo de código que ya está configurado en los archivos de directiva que concede a estas expresiones el **ejecución** permiso establecido de forma predeterminada. El grupo de código tiene un aspecto similar al siguiente:  
  
```  
<CodeGroup  
   class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="Execution"  
   Name="Report_Expressions_Default_Permissions"  
   Description="This code group grants default permissions for code in report expressions and Code element. ">  
    <IMembershipCondition  
       class="StrongNameMembershipCondition"  
       version="1"  
       PublicKeyBlob="002400..."  
    />  
</CodeGroup>  
```  
  
 **Ejecución** permiso permite al código para ejecutar (ejecutar), pero no para usar los recursos protegidos. Todas las expresiones incluidas en un informe se compilan en un ensamblado (denominado "ensamblado de expresiones") que se almacena como parte del informe compilado. Cuando se ejecuta el informe, el servidor de informes carga el ensamblado de expresiones y realiza llamadas a ese ensamblado para ejecutar expresiones. Los ensamblados de expresiones se firman con una clave concreta que se usa para definir el grupo de código para todos los ensamblados de expresiones.  
  
 Las expresiones de informe hacen referencia a las colecciones de modelos de objetos (campos, parámetros, etc.) y realizan tareas simples como operaciones de cadenas y aritméticas. Código que realiza estas operaciones simples solamente requiere **ejecución** permiso. De forma predeterminada, los métodos definidos por el usuario en el **código** elemento y los ensamblados personalizados se conceden **ejecución** permiso en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Así, para la mayoría de las expresiones, la configuración actual no requiere la modificación de ningún archivo de directiva de seguridad. Para conceder permisos adicionales a los ensamblados de expresiones, un administrador tiene que modificar los archivos de configuración de directivas del servidor de informes y el Diseñador de informes, y cambiar el grupo de código de expresiones de informe. Dado que es un valor global, el cambio de los permisos predeterminados para los ensamblados de expresiones afecta a todos los informes. Por esta razón, resulta muy recomendable que coloque todo el código que requiere seguridad adicional en un ensamblado personalizado. Solo a este ensamblado se le concederán los permisos que necesita.  
  
> [!IMPORTANT]  
>  El código que llama a ensamblados externos o a recursos protegidos debe incorporarse a un ensamblado personalizado para usarlo en informes. Al hacerlo, obtendrá más control sobre los permisos solicitados y validados por su código. No debe realizar llamadas para proteger métodos dentro de la **código** elemento. Si lo hace, debe conceder **FullTrust** para las expresiones de informe y concede acceso completo todo el código personalizado al CLR.  
  
> [!CAUTION]  
>  No conceda a **FullTrust** al grupo de código para expresiones de informe. Si lo hace, permitirá que todas las expresiones de informe realicen llamadas al sistema protegidas.  
  
## <a name="custom-assemblies-referenced-in-reports"></a>Ensamblados personalizados a los que se hace referencia en informes  
 Algunas expresiones de informes pueden llamar a ensamblados de terceros, también conocidos en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] como ensamblados personalizados. El servidor de informes espera estos ensamblados tengan al menos **ejecución** permiso en los archivos de configuración de directiva. De forma predeterminada, la directiva de archivos que se incluyen con [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] conceder **ejecución** permiso a todos los ensamblados a partir de la zona 'Mi PC'. Puede conceder permisos adicionales a ensamblados personalizados según sea necesario.  
  
 En algunos casos, puede que necesite realizar una operación que requiera permisos de código concretos en una expresión de informe. Normalmente, esto significa que una expresión de informe tiene que realizar una llamada a un método de biblioteca CLR protegido (como uno que tiene acceso a archivos o al Registro del sistema). La documentación de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] describe los permisos de código que se exigen para realizar esta llamada segura; para ejecutar la llamada, al código de llamada se le deben conceder estos permisos concretos y seguros. Si realiza la llamada desde una expresión de informe o el **código** elemento, el ensamblado de expresiones debe conceder los permisos adecuados. Sin embargo, una vez que concede los permisos al ensamblado de expresiones, a todo el código que se ejecuta en cualquier expresión de cualquier informe se le concede dicho permiso concreto. Es mucho más seguro realizar la llamada desde un ensamblado personalizado y conceder los permisos concretos a dicho ensamblado personalizado.  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de acceso del código en Reporting Services](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)   
 [Proteger desarrollo &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
