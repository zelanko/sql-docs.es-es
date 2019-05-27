---
title: Usar una conexión de modelo semántico de BI en Excel o Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 486195ca-530f-49e8-b40d-0f817db159ee
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a8e2b976fca00293d93cbf1e9987e115631bd81
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070930"
---
# <a name="use-a-bi-semantic-model-connection-in-excel-or-reporting-services"></a>Usar una conexión de modelo semántico de BI en Excel o Reporting Services
  Este tema explica cómo utilizar las conexiones de modelo semántico de BI creadas utilizando las instrucciones de otros temas. Si aún no ha creado un modelo semántico de BI, consulte [crear una conexión de modelo semántico de BI a un libro PowerPivot](create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md) y [crear una conexión de modelo semántico de BI a una base de datos de modelo Tabular](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="bkmk_connect"></a> Conexión de Excel  
 Puede especificar una conexión de modelo semántico de BI como origen de datos en Excel o cualquier otra aplicación empresarial que utilice datos de modelos tabulares de Analysis Services. En esta sección se explican los dos métodos para conectarse a los datos de modelo semántico de BI con Excel.  
  
 Las conexiones de modelo semántico de BI en Excel requieren que tenga Excel 2010 y el proveedor OLE DB MSOLAP.5 instalados en la estación de trabajo. Más adelante en esta sección se proporciona información adicional sobre los requisitos de conexión.  
  
 **Inicio desde SharePoint**  
  
-   Haga clic con el botón derecho en una conexión de modelo semántico de BI de una biblioteca y seleccione **Iniciar Excel**.  
  
 ![Comando de inicio rápido de la captura de pantalla de BISM](../media/ssas-bism-quicklaunch.gif "comando de inicio rápido de la captura de pantalla de BISM")  
  
 Haga clic en **Habilitar** cuando se le solicite para habilitar las conexiones de datos. Excel abre un libro que contiene una lista de campos de tabla dinámica rellena con los campos del origen de datos subyacente.  
  
 **Inicio desde Excel**  
  
1.  Inicie Excel y abra un libro. En la pestaña Datos, en el grupo Obtener datos externos, haga clic en **De otros orígenes**.  
  
2.  Haga clic en **Desde Analysis Services** y utilice el Asistente para la conexión de datos para importar los datos.  
  
3.  Escriba la dirección URL de SharePoint del archivo de conexión de modelo semántico de BI (por ejemplo,  **http://mysharepoint/shared compartidos/misdatos.bism**). Acepte la opción predeterminada de las credenciales de inicio de sesión, **Utilizar autenticación de Windows**. Haga clic en **Siguiente**.  
  
4.  En la siguiente página, haga clic en **Siguiente** de nuevo. Aunque se le pida que seleccione una base de datos, puede utilizar solo una base de datos especificada en la conexión de modelo semántico de BI.  
  
5.  En la última página, puede proporcionar un nombre descriptivo y una descripción. Haga clic en **Finalizar**y en **Aceptar** en el cuadro de diálogo Importar datos para importar los datos.  
  
 Para que las conexiones puedan establecerse, debe tener instalado Excel 2010 y el archivo MSOLAP.5.dll en el equipo cliente. Puede obtener el proveedor si instala la versión de PowerPivot para Excel que sea actual para esta versión o bien puede descargar únicamente el proveedor OLE DB de Analysis Services desde el [página de descarga de Feature Pack](https://go.microsoft.com/fwlink/?linkid=214066).  
  
 Para confirmar que MSOLAP.5.dll es la versión actual, examine `HKEY_CLASSES_ROOT\MSOLAP` en el Registro. `CurVer` se debe establecer en MSOLAP.5.  
  
 También debe tener permisos de lectura en el archivo de modelo semántico de BI en SharePoint. Los permisos de lectura incluyen los derechos de descarga. Excel descarga la información de conexión de modelo semántico de BI desde SharePoint y abre una conexión directa a la base de datos mediante `HTTP Get`. Las solicitudes de conexión no pasan por SharePoint una vez que la información de conexión de modelo semántico de BI se almacena localmente.  
  
 Si se va a conectar a una base de datos de modelo tabular que se ejecute en un servidor de Analysis Services, los permisos de SharePoint no son suficientes. También debe tener permisos de lectura en la base de datos del servidor. Este paso se debe haber realizado al crear la conexión de modelo semántico de BI. Para obtener más información, vea [Crear una conexión de modelo semántico de BI a una base de datos de modelo tabular](create-a-bi-semantic-model-connection-to-a-tabular-model-database.md).  
  
##  <a name="bkmk_use"></a> Conexión desde Reporting Services en SharePoint  
 Puede utilizar una conexión de modelo semántico de BI de la misma forma que para la mayoría de los orígenes de datos, especificando el archivo como origen de datos en el documento o la herramienta que utilice los datos. Aunque una conexión de modelo semántico de BI señala a una base de datos física en otro servidor, utilice el archivo de conexión usa como si fuera el origen de datos. La dirección URL de SharePoint de BI de la conexión de modelo semántico de BI es una ubicación válida de origen de datos para informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] que utilicen datos de modelo semántico de BI.  
  
 En el diseño de informes ad hoc en SharePoint, el usuario que cree el informe debe tener permisos de SharePoint en el archivo de conexión de modelo semántico de BI (.bism) y en la base de datos de modelo semántico de Business Intelligence. El contexto de seguridad de la conexión es el usuario interactivo que crea el informe.  
  
  
