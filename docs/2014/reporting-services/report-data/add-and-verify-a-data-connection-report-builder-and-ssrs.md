---
title: Agregar y comprobar una conexión de datos o un origen de datos (generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 60c12e1ea7f184770d07fcd4af42b81ca41d13db
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082024"
---
# <a name="add-and-verify-a-data-connection-or-data-source-report-builder-and-ssrs"></a>Agregar y comprobar una conexión de datos o un origen de datos (generador de informes y SSRS)
  En el Generador de informes, puede agregar un origen de datos compartido del servidor de informes o crear un origen de datos incrustado para el informe. En el Diseñador de informes, puede crear un origen de datos compartido o un origen de datos incrustado e implementarlo en un servidor de informes.  
  
 Para agregar un origen de datos compartido al informe, busque un servidor de informes y seleccione un origen de datos compartido. El origen de datos compartido del informe señala a la definición del origen de datos compartido en el servidor de informes.  
  
 Para crear un origen de datos incrustado, debe disponer de la información de la conexión al origen de datos externo y saber qué permisos necesita para el acceso a los datos. Esta información normalmente procede del propietario del origen de datos. Puede probar la conexión para comprobar que las credenciales que se especifican son suficientes.  
  
 Para obtener más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión (Generador de informes y SSRS)](../data-connections-data-sources-and-connection-strings-in-report-builder.md) y [Especificar credenciales en el Generador de informes](../specify-credentials-in-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-reference-to-a-shared-data-source"></a>Para crear una referencia a un origen de datos compartido  
  
1.  En la barra de herramientas del panel Datos de informe, haga clic en **Nuevo** y, a continuación, haga clic en **Origen de datos**. Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
2.  En el cuadro de texto **Nombre** , escriba un nombre para el origen de datos.  
  
    > [!NOTE]  
    >  Este nombre se guarda en la definición de informe local. No es el nombre del origen de datos compartido del servidor de informes.  
  
3.  Seleccione **Usar una conexión compartida en el modelo de informe**. Aparece la lista de modelos de informe y orígenes de datos compartidos usados recientemente. Para seleccionar uno de un servidor de informes, haga clic en **Examinar** y busque la carpeta del servidor de informes en la que están disponibles los orígenes de datos compartidos.  
  
4.  Seleccione el origen de datos compartido y, a continuación, haga clic en **Abrir**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 El origen de datos aparece en el panel Datos de informe.  
  
### <a name="to-create-an-embedded-data-source"></a>Para crear un origen de datos incrustado  
  
1.  En la barra de herramientas del panel Datos de informe, haga clic en **Nuevo**y, a continuación, haga clic en **Origen de datos**. Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
2.  En el cuadro de texto **Nombre** , escriba un nombre para el origen de datos o acepte el valor predeterminado.  
  
3.  Compruebe que la casilla **Usar una conexión incrustada en el informe** está seleccionada.  
  
    1.  En la lista desplegable **Seleccionar el tipo de conexión** , seleccione un tipo de origen de datos (por ejemplo, **Microsoft SQL Server** o **OLE DB**).  
  
    2.  Especifique una cadena de conexión usando una de las alternativas siguientes:  
  
    -   Escriba la cadena de conexión directamente en el cuadro de texto **Cadena de conexión** . Para obtener una lista de cadenas de conexión de ejemplo, vea [conexiones de datos, orígenes de datos y cadenas de conexión en el generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
    -   Haga clic en el botón de expresión (**fx** ) para crear una expresión que dé como resultado una cadena de conexión. En el cuadro de diálogo **Expresión** , escriba la expresión en el panel Expresión. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    -   Haga clic en **Generar** para abrir el cuadro de diálogo **Propiedades de conexión** correspondiente al tipo de origen de datos que eligió en el paso 2.  
  
         Rellene los campos del cuadro de diálogo **Propiedades de conexión** según corresponda para el tipo de origen de datos. Las propiedades de conexión incluyen el tipo de origen de datos, el nombre del origen de datos, y las credenciales que se deben usar. Después de especificar los valores en este cuadro de diálogo, haga clic en **Probar conexión** para comprobar que el origen de datos está disponible y que las credenciales que especificó son correctas.  
  
4.  Haga clic en **Credenciales**.  
  
     Especifique las credenciales que se deben usar para este origen de datos. El propietario del origen de datos elige el tipo de credenciales que se admiten. En algunos casos, el propietario del origen de datos mantiene un origen de datos compartido en un servidor de informes y configura el origen de datos con credenciales que puede utilizar. Póngase en contacto con el propietario del origen de datos para obtener esta información. Para más información, vea [Especificar credenciales en el Generador de informes](../specify-credentials-in-report-builder.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 El origen de datos aparece en el panel Datos de informe.  
  
### <a name="to-verify-a-data-connection"></a>Para comprobar una conexión de datos  
  
1.  En la barra de herramientas del panel Datos de informe, haga doble clic en el origen de datos. Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
2.  Haga clic en **Probar conexión**.  
  
3.  Si la conexión es correcta, aparece el mensaje siguiente: "Conexión creada correctamente". [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Si la conexión no es correcta, aparece un mensaje similar al siguiente: "No se puede establecer conexión con el origen de datos".  
  
5.  Haga clic en **Detalles**y utilice la información para corregir el problema.  
  
     Para más información, vea [Especificar credenciales en el Generador de informes](../specify-credentials-in-report-builder.md).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-datasets-ssrs.md)   
 [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
  
