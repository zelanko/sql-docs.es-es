---
title: Propiedades del origen de datos (cuadro de diálogo), general (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10018"
ms.assetid: b956f43a-8426-4679-acc1-00f405d5ff5b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7bedf016dce02928bbd47dbfce60943ec667a824
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109471"
---
# <a name="data-source-properties-dialog-box-general-report-builder"></a>Propiedades del origen de datos (cuadro de diálogo), General (Generador de informes)
  Seleccione **General** en el cuadro de diálogo **Propiedades del origen de datos** para seleccionar un origen de datos compartido desde un servidor de informes o para crear o modificar información de conexión de un origen de datos incrustado en el informe.  
  
 El tipo de credenciales utilizado para conectarse a un origen de datos se especifica en las propiedades del origen de datos. Al abrir un informe desde el servidor de informes, las credenciales en tiempo de ejecución, especificadas en las propiedades de origen de datos de un informe, podrían no funcionar en las tareas de tiempo de diseño como la creación de consultas y la obtención de una vista previa de los informes. Por ejemplo, el origen de datos podría usar credenciales de Windows distintas a las suyas o un nombre de usuario y contraseña que le son desconocidas.  
  
 El Generador de informes abre el cuadro de diálogo **Escribir credenciales de origen de datos** cuando no puede conectarse al origen de datos con las credenciales proporcionadas en las propiedades del origen de datos. Normalmente esto sucede cuando:  
  
-   El origen de datos está configurado para pedir credenciales.  
  
-   El origen de datos está configurado para almacenar credenciales.  Para minimizar las posibles amenazas de seguridad, el Generador de informes está diseñado para no recuperar credenciales almacenadas en el servidor.  
  
 Puede usar el cuadro de diálogo **Escribir credenciales de origen de datos** para cambiar las credenciales que usa el Generador de informes en el tiempo de diseño para conectarse al origen de datos o el usuario de Windows actual o proporcionar un nombre de usuario y una contraseña. Si proporciona un nombre de usuario y una contraseña puede indicar si se usan como credenciales de Windows.  
  
> [!NOTE]  
>  Aunque los diseñadores de consultas permiten especificar otro tipo para las credenciales de tiempo de diseño, la vista previa de informe solo permite especificar el nombre de usuario y la contraseña de las opciones de credenciales existentes especificadas en el origen de datos.  
  
 Al hacer clic en **Probar conexión**, la conexión al origen de datos se prueba con las credenciales especificadas en la página de credenciales de propiedades del origen de datos. Puede probar las conexiones a los orígenes de datos incrustados y compartidos.  
  
 Si las credenciales especificadas están incompletas (por ejemplo, se requiere una contraseña), el Generador de informes vuelve a solicitar las credenciales de tiempo de ejecución cuando es necesario conectarse al origen de datos. Las credenciales de tiempo de diseño están almacenadas y no se solicitan de nuevo.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba el nombre del origen de datos. Dicho nombre debe ser único en el informe. De forma predeterminada, al origen de datos se le asigna un nombre general, como DataSource1 o DataSource2.  
  
 **Usar una conexión compartida**  
 Seleccione esta opción para ir a un origen de datos compartido publicado en un servidor de informes.  
  
 Una vez seleccionado el origen de datos de un servidor de informes, el Generador de informes mantiene una conexión a dicho servidor.  
  
 **Usar una conexión incrustada en mi informe**  
 Seleccione esta opción para crear un origen de datos que únicamente use este informe.  
  
 **Tipo**  
 Seleccione una extensión de procesamiento de datos. En la lista se muestran todas las extensiones registradas.  
  
 **Cadena de conexión**  
 Escriba una cadena de conexión para el origen de datos. Haga clic en **Generar** para generar la cadena de conexión mediante el cuadro de diálogo **Propiedades de conexión** . Haga clic en el botón **Expresiones** (*fx*) para editar la expresión.  
  
 **Usar una sola transacción al procesar las consultas**  
 Seleccione esta opción para indicar que los conjuntos de datos que usan este origen de datos deben ejecutarse en una sola transacción en la base de datos. Para incluir transacciones para subinformes que usan el mismo origen de datos, seleccione el subinforme y, en el panel de propiedades, establezca **MergeTransactions** en **True**.  
  
 **Probar conexión**  
 Haga clic para comprobar que la conexión del origen de datos funciona con las credenciales especificadas. Si no se puede realizar la conexión, debe comprobar las credenciales y la disponibilidad del servidor. Puede probar las conexiones de origen de datos para los orígenes de datos incrustados y compartidos.  
  
## <a name="see-also"></a>Consulte también  
 [Agregar datos a un informe &#40;Generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Generador de informes](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Propiedades del origen de datos (cuadro de diálogo), credenciales &#40;Generador de informes&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md)   
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
