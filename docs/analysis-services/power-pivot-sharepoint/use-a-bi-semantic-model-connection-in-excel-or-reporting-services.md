---
title: "Usar una conexión de modelo semántico de BI en Excel o Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 486195ca-530f-49e8-b40d-0f817db159ee
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8fc3d2ae19c9b8237593d1b4e1b559f22c5da1ed
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="use-a-bi-semantic-model-connection-in-excel-or-reporting-services"></a>Usar una conexión de modelo semántico de BI en Excel o Reporting Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Este tema explica cómo utilizar las conexiones de modelo semántico de BI creadas utilizando las instrucciones de otros temas. Si aún no ha creado un modelo semántico de BI, vea [Crear una conexión de modelo semántico de BI a un libro PowerPivot](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md) y [Crear una conexión de modelo semántico de BI a una base de datos de modelo tabular](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="bkmk_connect"></a> Conexión de Excel  
 Puede especificar una conexión de modelo semántico de BI como origen de datos en Excel o cualquier otra aplicación empresarial que utilice datos de modelos tabulares de Analysis Services. En esta sección se explican los dos métodos para conectarse a los datos de modelo semántico de BI con Excel.  
  
 Las conexiones de modelo semántico de BI en Excel requieren que tenga Excel 2010 y el proveedor OLE DB MSOLAP.5 instalados en la estación de trabajo. Más adelante en esta sección se proporciona información adicional sobre los requisitos de conexión.  
  
 **Inicio desde SharePoint**  
  
-   Haga clic con el botón derecho en una conexión de modelo semántico de BI de una biblioteca y seleccione **Iniciar Excel**.  
  
 ![Comando de inicio rápido de captura de pantalla de BISM](../../analysis-services/power-pivot-sharepoint/media/ssas-bism-quicklaunch.gif "comando de inicio rápido de captura de pantalla de BISM")  
  
 Haga clic en **Habilitar** cuando se le solicite para habilitar las conexiones de datos. Excel abre un libro que contiene una lista de campos de tabla dinámica rellena con los campos del origen de datos subyacente.  
  
 **Inicio desde Excel**  
  
1.  Inicie Excel y abra un libro. En la pestaña Datos, en el grupo Obtener datos externos, haga clic en **De otros orígenes**.  
  
2.  Haga clic en **Desde Analysis Services** y utilice el Asistente para la conexión de datos para importar los datos.  
  
3.  Escriba la dirección URL de SharePoint del archivo de conexión de modelo semántico de BI (por ejemplo, `http://mysharepoint/shared documents/myData.bism`). Acepte la opción predeterminada de las credenciales de inicio de sesión, **Utilizar autenticación de Windows**. Haga clic en **Siguiente**.  
  
4.  En la siguiente página, haga clic en **Siguiente** de nuevo. Aunque se le pida que seleccione una base de datos, puede utilizar solo una base de datos especificada en la conexión de modelo semántico de BI.  
  
5.  En la última página, puede proporcionar un nombre descriptivo y una descripción. Haga clic en **Finalizar**y en **Aceptar** en el cuadro de diálogo Importar datos para importar los datos.  
  
 Para que las conexiones puedan establecerse, debe tener instalado Excel 2010 y el archivo MSOLAP.5.dll en el equipo cliente. Puede obtener el proveedor si instala la versión de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel que sea actual para esta versión o descargar únicamente el proveedor OLE DB de Analysis Services en la [página de descarga de Feature Pack](http://go.microsoft.com/fwlink/?linkid=214066).  
  
 Para confirmar que MSOLAP.5.dll es la versión actual, examine **HKEY_CLASSES_ROOT\MSOLAP** en el Registro. **CurVer** se debe establecer en MSOLAP.5.  
  
 También debe tener permisos de lectura en el archivo de modelo semántico de BI en SharePoint. Los permisos de lectura incluyen los derechos de descarga. Excel descarga la información de conexión de modelo semántico de BI desde SharePoint y abre una conexión directa a la base de datos mediante **HTTP Get**. Las solicitudes de conexión no pasan por SharePoint una vez que la información de conexión de modelo semántico de BI se almacena localmente.  
  
 Si se va a conectar a una base de datos de modelo tabular que se ejecute en un servidor de Analysis Services, los permisos de SharePoint no son suficientes. También debe tener permisos de lectura en la base de datos del servidor. Este paso se debe haber realizado al crear la conexión de modelo semántico de BI. Para obtener más información, vea [Crear una conexión de modelo semántico de BI a una base de datos de modelo tabular](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="bkmk_use"></a> Conexión desde Reporting Services en SharePoint  
 Puede utilizar una conexión de modelo semántico de BI de la misma forma que para la mayoría de los orígenes de datos, especificando el archivo como origen de datos en el documento o la herramienta que utilice los datos. Aunque una conexión de modelo semántico de BI señala a una base de datos física en otro servidor, utilice el archivo de conexión usa como si fuera el origen de datos. La dirección URL de SharePoint de BI de la conexión de modelo semántico de BI es una ubicación válida de origen de datos para informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] que utilicen datos de modelo semántico de BI.  
  
 En el diseño de informes ad hoc en SharePoint, el usuario que cree el informe debe tener permisos de SharePoint en el archivo de conexión de modelo semántico de BI (.bism) y en la base de datos de modelo semántico de Business Intelligence. El contexto de seguridad de la conexión es el usuario interactivo que crea el informe.  
  
  
