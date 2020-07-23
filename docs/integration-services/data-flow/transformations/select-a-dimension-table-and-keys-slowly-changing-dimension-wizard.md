---
title: Seleccionar una tabla de dimensiones y claves (Asistente para dimensión de variación lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.selecttableandkeys.f1
ms.assetid: 01e0495f-de35-4607-ba19-0539e801e8fd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 48d0d57c66a05a28a41de37b6bea0867fbe2c8e5
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919502"
---
# <a name="select-a-dimension-table-and-keys-slowly-changing-dimension-wizard"></a>Seleccionar una tabla de dimensiones y claves (Asistente para dimensión de variación lenta)

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilice la página **Seleccionar una tabla de dimensiones y claves** para seleccionar una tabla de dimensiones para cargar. Asigne columnas del flujo de datos a las columnas que se van a cargar.  
  
 Para obtener más información acerca de este asistente, vea [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opciones  
 **Connection manager**  
 Seleccione un administrador de conexiones OLE DB existente de la lista o haga clic en **Nuevo** para crear uno nuevo.  
  
> [!NOTE]  
>  El Asistente para dimensiones de variación lenta solamente admite los administradores de conexiones OLE DB y las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Nuevo**  
 Use el cuadro de diálogo **Configurar el administrador de conexiones OLE DB** para seleccionar un administrador de conexiones existente o haga clic en **Nuevo** para crear una nueva conexión OLE DB.  
  
 **Tabla o vista**  
 Seleccione una tabla o una vista de la lista.  
  
 **Columnas de entrada**  
 Seleccione las columnas de la lista de columnas de entrada para las que desea especificar asignaciones.  
  
 **Columnas de dimensión**  
 Muestra todas las columnas de dimensión disponibles.  
  
 **Tipo de clave**  
 Seleccione una de las columnas de dimensión para que sea la clave empresarial. Es necesario disponer de una clave empresarial.  
  
## <a name="see-also"></a>Consulte también  
 [Configuración de salidas con el Asistente para dimensiones de variación lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
