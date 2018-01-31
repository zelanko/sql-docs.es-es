---
title: Generar scripts (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9711c617-3c68-4e5a-aea3-befc64d51524
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d1afb1297566bb7f203956d24b0ea62b56817d28
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="generate-scripts-sql-server-management-studio"></a>Generar scripts (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] proporciona dos mecanismos para generar scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Puede crear scripts para varios objetos con el **Asistente Generar y publicar scripts**. También puede generar un script para objetos individuales o varios objetos con el menú **Incluir como** del **Explorador de objetos**.  
  
1.  **Elegir un método:**  [Asistente generar y publicar scripts](#GenPubScriptWiz), [Menú Incluir como del Explorador de objetos](#OEScriptAsMenu)  
  
2.  **Para usar el script como menú:**  [Generar un script de un solo objeto](#ScriptSingleObject), [Generar un script de dos objetos mediante el Explorador de objetos](#ScriptTwoObjectsOE), [Generar un script de dos objetos usando los detalles del Explorador de objetos](#ScriptTwoObjectsOED)  
  
## <a name="before-you-begin"></a>Antes de comenzar  
 Elija el mecanismo que mejor cumpla sus requisitos.  
  
###  <a name="GenPubScriptWiz"></a> Asistente generar y publicar scripts  
 Use el **Asistente Generar y publicar scripts** para crear un script [!INCLUDE[tsql](../../includes/tsql-md.md)] para muchos objetos. El asistente genera un script de todos los objetos de una base de datos o un subconjunto de los objetos que seleccione. El asistente dispone de muchas opciones para los scripts, como la posibilidad de incluir permisos, la intercalación, las restricciones, etc. Para obtener instrucciones acerca de cómo usar el asistente, vea [Generate and Publish Scripts Wizard](../../relational-databases/scripting/generate-and-publish-scripts-wizard.md).  
  
###  <a name="OEScriptAsMenu"></a> Menú Incluir como del Explorador de objetos  
 Puede usar el menú **Incluir como del Explorador de objetos** para generar un script de un solo objeto, de varios objetos o de varias instrucciones para un único objeto. Puede elegir uno de varios tipos de scripts; por ejemplo crear, modificar o quitar el objeto. Puede guardar un script en una ventana del Editor de consultas, en un archivo o en el Portapapeles. El script se crea en formato Unicode.  
  
##  <a name="ScriptSingleObject"></a> Para generar un script de un solo objeto  
 **Para generar un script de un solo objeto**  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, y a continuación expanda la base de datos que contiene el objeto que se debe incluir en un script.  
  
3.  Expanda la categoría del objeto. Por ejemplo, expanda el nodo **Vistas** o **Tablas** .  
  
4.  Haga clic con el botón derecho en el objeto y vaya a **Incluir \<tipo de objeto> como**; por ejemplo, vaya a **Incluir tabla como**.  
  
5.  Seleccione el tipo de script, como **Create to** o **Alter to**.  
  
6.  Seleccione la ubicación para guardar el script, como **Nueva ventana del Editor de consultas** o **Portapapeles**.  
  
##  <a name="ScriptTwoObjectsOE"></a> Para generar un script de dos objetos usando el Explorador de objetos  
 **Para generar un script de dos objetos usando el Explorador de objetos**  
  
 En ocasiones, es posible que necesite un script que ofrezca varias opciones como, por ejemplo, quitar un procedimiento y, a continuación, crear otro, o bien crear una tabla y modificarla posteriormente. Los siguientes procesos de generación de scripts de varios objetos también funcionan si necesita crear un script que haga referencia a tipos diferentes de objetos, como tablas, vistas y procedimientos almacenados.  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, y a continuación expanda la base de datos que contiene los objetos que se deben incluir en un script.  
  
3.  Haga clic con el botón derecho en el primer objeto que quiere incluir en un script, vaya a **Incluir \<tipo de objeto> como** y, en las selecciones **Guardar como**, elija **Nueva ventana del Editor de consultas** como el destino de salida.  
  
4.  Navegue hasta el segundo objeto que desea incluir en el script.  
  
5.  Haga clic con el botón derecho en el objeto, vaya a **Incluir \<tipo de objeto> como** y, en las selecciones **Guardar como**, elija **Portapapeles** como el destino de salida.  
  
6.  En la ventana Editor de consultas abierta para el primer objeto, pegue el script para el segundo objeto del Portapapeles.  
  
##  <a name="ScriptTwoObjectsOED"></a> Para generar un script de dos objetos usando Detalles del Explorador de objetos.  
 **Para generar un script de dos objetos usando Detalles del Explorador de objetos**  
  
 Puede usar el panel **Detalles del Explorador de objetos** para generar un script para varios objetos de la misma categoría.  
  
1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, y a continuación expanda la base de datos que contiene los objetos que se deben incluir en un script.  
  
3.  Expanda el nodo de categoría de los tipos de objeto que desea incluir en el script, como el nodo **Tablas** .  
  
4.  Abra el panel **Detalles del Explorador de objetos** seleccionando **F7**o abriendo el menú **Ver** y seleccionando **Detalles del Explorador de objetos**.  
  
5.  Haga clic con el botón primario en uno de los objetos que desea incluir en el script.  
  
6.  Presione Crtl y haga clic con el botón primario en el segundo objeto que desea incluir en el script.  
  
7.  Haga clic con el botón derecho en uno de los objetos seleccionados y elija **Incluir \<tipo de objeto> como**.  
  
  
