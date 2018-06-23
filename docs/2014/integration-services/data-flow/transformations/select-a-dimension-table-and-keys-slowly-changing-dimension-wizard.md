---
title: Seleccionar una tabla de dimensiones y claves (Asistente para dimensión de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9a62ab620db99e06f4e971e4bfe488f1741dd510
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201633"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>Seleccionar una tabla de dimensiones y claves (Asistente para dimensión de variación lenta)
  Utilice la página **Seleccionar una tabla de dimensiones y claves** para seleccionar una tabla de dimensiones para cargar. Asigne columnas del flujo de datos a las columnas que se van a cargar.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Connection manager**  
 Seleccione un administrador de conexiones OLE DB existente de la lista o haga clic en **Nuevo** para crear uno nuevo.  
  
> [!NOTE]  
>  El Asistente para dimensiones de variación lenta solamente admite los administradores de conexiones OLE DB y las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Nueva**  
 Use el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** para seleccionar un administrador de conexiones existente o haga clic en **Nuevo** para crear una nueva conexión OLE DB.  
  
 **Tabla o vista**  
 Seleccione una tabla o una vista de la lista.  
  
 **Columnas de entrada**  
 Seleccione las columnas de la lista de columnas de entrada para las que desea especificar asignaciones.  
  
 **Columnas de dimensión**  
 Muestra todas las columnas de dimensión disponibles.  
  
 **Tipo de clave**  
 Seleccione una de las columnas de dimensión para que sea la clave empresarial. Es necesario disponer de una clave empresarial.  
  
## <a name="see-also"></a>Vea también  
 [Configuración de salidas con el Asistente para dimensiones de variación lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  