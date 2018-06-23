---
title: 'Tarea 10: Agregar la transformación Agrupación aproximada para identificar duplicados | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cf9ad3dff4737d7308e7ec3434985b18015f29d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111932"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>Tarea 10: agregar la transformación Agrupación aproximada para identificar duplicados
  En esta tarea, agregará una transformación Agrupación aproximada al flujo de datos. La transformación Agrupación aproximada puede ayudar a identificar duplicados en los datos de origen. Vea [la transformación Agrupación aproximada](http://msdn.microsoft.com/library/ms141764.aspx) para obtener más detalles.  
  
1.  Arrastrar y colocar **agrupación aproximada** transformar en **otras transformaciones** en el **cuadro de herramientas de SSIS** a la **de flujo de datos** en la ficha  **Combinar registros correctos y corregidos**.  
  
2.  Haga clic en **agrupación aproximada** transformar en el **de flujo de datos** ficha y haga clic en **cambiar el nombre de**. Tipo de **agrupar proveedores con Id. coincidentes** y presione **ENTRAR**.  
  
3.  Conectar **combinar registros correctos y corregidos** a **agrupar proveedores con Id. coincidentes** mediante el conector azul.  
  
     ![Conexión a agrupar proveedores con Id. coincidentes](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "conexión para agrupar proveedores con Id. coincidentes")  
  
4.  Haga doble clic en **agrupar proveedores con Id. coincidentes**.  
  
5.  En el **Editor de transformación Agrupación aproximada**, haga clic en **New** junto a **lista desplegable de OLE DB Connection Manager** para iniciar **configurar conexiones OLE DB Administrador de** cuadro de diálogo.  
  
6.  En el cuadro de diálogo, haga clic en **New** para iniciar **Connection Manager** cuadro de diálogo.  
  
7.  Tipo de **(local)** o **período** (.) para el nombre del servidor.  
  
8.  Seleccione **MDS** para **seleccione o escriba un nombre de base de datos** campo. Va a usar la base de datos MDS como almacenamiento temporal para la **transformación Agrupación aproximada**. El **agrupación aproximada** transformación requiere una conexión a una instancia de SQL Server para crear las tablas temporales de SQL Server que necesita el algoritmo de transformación para realizar su trabajo. Puede crear una base de datos o usar otra base de datos existente con este fin.  
  
9. Haga clic en **Probar conexión** para probar la conexión y haga clic en **Aceptar** en el cuadro de mensaje.  
  
10. En el **Connection Manager** cuadro de diálogo, haga clic en **Aceptar**.  
  
11. Seleccione **(local). MDS** (o **localhost. MDS**) desde el **lista de conexiones de datos** y haga clic en **Aceptar**.  
  
12. En el **Editor de transformación Agrupación aproximada**, confirme que **(local). MDS** o **localhost. MDS** está seleccionada para la **OLE DB Connection Manager**.  
  
13. Cambie a la **columnas** ficha.  
  
14. Seleccione (casilla) **SupplierID_Output** en la lista de **columnas de entrada disponibles**. Para configurar la transformación, seleccione las columnas de entrada que se usarán al identificar duplicados. Por simplificar, use solo la columna SupplierID en este paso.  
  
     ![Editor de transformación Agrupación aproximada](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "Editor de transformación Agrupación aproximada")  
  
15. Haga clic en **Aceptar** para cerrar el **Editor de transformación Agrupación aproximada**.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 11: Agregar la transformación División condicional para filtrar duplicados](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  