---
title: Informes, elementos de informe y definiciones de informe (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report definitions
- reports
ms.assetid: 2d746550-f8cc-4e97-8a06-d0f03cffc18d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d22c8c22170ecef301eacd553f15c16091c9a6e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105052"
---
# <a name="reports-report-parts-and-report-definitions-report-builder-and-ssrs"></a>Informes, elementos de informe y definiciones de informe (Generador de informes y SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]usa diversos términos para describir un informe en distintos Estados, incluida la definición inicial, el informe publicado y el informe visualizado tal como aparece para el usuario.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-rdl-files"></a>Archivos de definición de informe (.rdl)  
 Una definición de informe es un archivo que se crea mediante el Generador de informes o el Diseñador de informes. Esta definición proporciona una descripción completa de conexiones a orígenes de datos, consultas usadas para recuperar datos, expresiones, parámetros, imágenes, cuadros de texto, tablas y cualquier otro elemento de tiempo de diseño que se pudiera incluir en un informe. Si bien las definiciones de informe pueden ser complejas, como mínimo especifican una consulta y otro contenido del informe, las propiedades del informe y un diseño de informe.  
  
 Las definiciones de informe se representan en tiempo de ejecución como un informe procesado. En ese momento, los datos se recuperan del origen de datos con el formato definido en las instrucciones de la definición de informe. Una definición de informe puede ejecutarse directamente en un equipo y guardarse localmente o puede publicarse en un servidor de informes para que otros también la ejecuten.  
  
 Las definiciones de informe se escriben en XML de conformidad con una gramática XML denominada lenguaje RDL (Report Definition Language). El lenguaje RDL describe los elementos XML, que engloban todas las variantes posibles que puede tener un informe.  
  
## <a name="client-report-definition-rdlc-files"></a>Archivos de definición de informe de cliente (.rdlc).  
 El Diseñador de informes de Visual Studio genera archivos de definición de informe de cliente (.rdlc) para su uso con el control ReportViewer. Los archivos .rdlc se pueden convertir en archivos .rdl para usarlos con el Diseñador de informes de Reporting Services.  
  
## <a name="report-part-rsc-files"></a>Archivos de elementos de informe (.rsc)  
 Una definición de elemento de informe es un fragmento de XML de un archivo de definición de informe. Los elementos de informe se crean mediante una definición de informe y, a continuación, seleccionando elementos de informe en el informe para su publicación por separado como elementos de informe. Son elementos de informe las regiones de datos, los rectángulos y los elementos que contienen, y las imágenes. Puede guardar un elemento de informe con sus conjuntos de datos dependientes y referencias a orígenes de datos compartidos para que se puedan volver a usar en otros informes.  
  
 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
## <a name="published-reports"></a>Informes publicados  
 Después de crear un archivo .rdl, puede guardarlo localmente o en una carpeta personal (como la carpeta Mis informes) en el servidor de informes. Cuando el informe esté listo para que los consulten otros usuarios, debe guardarlo en el Generador de informes y publicarlo en una carpeta pública del servidor de informes. Lo puede cargar mediante el Administrador de informes o implementando una solución de proyecto de informe en el Diseñador de informes. Un informe publicado es un elemento que se almacena en una base de datos del servidor de informes y se administra en un servidor de informes o en un sitio de SharePoint.  
  
 Un informe publicado se protege mediante asignaciones de roles utilizando el modelo de seguridad basada en roles de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se tiene acceso a los informes publicados a través de direcciones URL, elementos web de SharePoint o del Administrador de informes. También se puede navegar a ellos y abrirlos en el Generador de informes.  
  
### <a name="report-snapshots"></a>Instantáneas de informe  
 Un informe también se puede publicar como una instantánea que contiene la información de presentación y los datos tal como estaban cuando se ejecutó inicialmente el informe. Las instantáneas de informe no se guardan con un formato de representación concreto. En su lugar, las instantáneas de informe se representan en un formato de visualización final (como HTML) solo cuando un usuario o una aplicación lo solicita. Para más información, vea [Buscar y ver informes en el Administrador de informes &#40;Generador de informes y SSRS&#41;](../report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md).  
  
## <a name="rendered-reports"></a>Informes representados  
 Un informe representado es un informe totalmente procesado que contiene datos e información de diseño en un formato que permite su visualización (por ejemplo, HTML). Un informe no puede visualizarse hasta que no se haya representado en un formato de salida. Puede representar un informe realizando una de las siguientes acciones:  
  
-   Cree o abra un informe en el Generador de informes o el Diseñador de informes y ejecútelo.  
  
-   Busque y ejecute un informe en el Administrador de informes.  
  
-   Busque y ejecute un informe en un sitio de SharePoint que esté integrado con un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Suscríbase a un informe, que se entrega a una bandeja de entrada de correo electrónico o a un recurso compartido de archivos en un formato de salida que especifique.  
  
 Suscribirse a un informe, que se entrega a una bandeja de entrada de correo electrónico o a un recurso compartido de archivos en un formato que especifique. El formato de representación predeterminado para un informe es HTML 4.0. Además del formato HTML, los informes se pueden representar en varios formatos de salida, entre los que se incluyen Excel, Word, XML, PDF, TIFF y CSV. Al igual que ocurre con los informes publicados, los informes representados no se pueden editar ni volver a guardar en el servidor de informes. Para obtener más información, vea [exportar informes &#40;generador de informes y SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos de creación de informes &#40;Generador de informes y SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [Generador de informes en SQL Server 2014](../report-builder/report-builder-in-sql-server-2016.md)   
 [Instalación, desinstalación y compatibilidad Generador de informes](../install-uninstall-and-report-builder-support.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportar informes &#40;Generador de informes y SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
