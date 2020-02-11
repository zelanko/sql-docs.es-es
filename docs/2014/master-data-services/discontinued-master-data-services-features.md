---
title: Características de Master Data Services no incluidas en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3f1eb85cb05c8284990d46241ed752515ef5504b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479442"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>Características descontinuadas de Master Data Services en SQL Server 2014
  Este tema describe las características de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que ya no están disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="includesssql14includessssql14-mdmd-discontinued-features"></a>
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Características no incluidas  
 Hay características que no se incluyen en esta versión.  
  
## <a name="includesssql11includessssql11-mdmd-discontinued-features"></a>
  [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Características no incluidas  
  
### <a name="security"></a>Seguridad  
 Para facilitar la seguridad de asignación, ya no se pueden asignar permisos de objeto del modelo a la jerarquía derivada, la jerarquía explícita y los objetos del grupo de atributos.  
  
-   Los permisos de jerarquía derivada se basan ahora en el modelo. Por ejemplo, si desea que un usuario tenga permiso para una jerarquía derivada, debe asignar la **actualización** al objeto de modelo. A continuación, puede asignar **denegar** el acceso a las entidades a las que no desea que el usuario tenga acceso.  
  
-   Los permisos de jerarquía explícita se basan ahora en la entidad. Por ejemplo, si el usuario tiene permisos de **actualización** en una entidad de cuenta, todas las jerarquías explícitas de la entidad serán actualizables.  
  
-   Los permisos de grupo de atributos ya no se pueden asignar en el área funcional **permisos de usuario y de grupo** . En su lugar, en el área funcional de **Administración del sistema** donde se crean los grupos de atributos, se puede conceder a los usuarios y grupos el permiso **Actualizar** para los grupos de atributos. **El permiso de solo lectura** para los grupos de atributos ya no está disponible.  
  
### <a name="staging-process"></a>Proceso de almacenamiento provisional  
 No puede usar el nuevo proceso de almacenamiento provisional para:  
  
-   Crear o eliminar colecciones.  
  
-   Agregar o quitar miembros de colecciones.  
  
-   Reactivar miembros y colecciones.  
  
 Puede usar el proceso de almacenamiento provisional de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] para trabajar con colecciones.  
  
### <a name="model-deployment-wizard"></a>Asistente para la implementación de modelos  
 Los paquetes que contienen datos ya no se pueden crear e implementar mediante el asistente en la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. En su lugar se puede usar una nueva utilidad de la línea de comandos. Para obtener más información, consulte [Implementar modelos &#40;Master Data Services&#41;](deploying-models-master-data-services.md).  
  
 El asistente se puede seguir usando para crear e implementar paquetes que no contienen datos.  
  
 Además, los paquetes solamente se pueden implementar en la edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en la que se crearon. Esto significa que los paquetes que se hayan creado en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] no se pueden implementar en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Debe implementar el paquete en un entorno de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] y, posteriormente, actualizar la base de datos a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
### <a name="code-generation-business-rules"></a>Reglas de negocios de generación de código  
 Las reglas de negocios que generan valores automáticamente para el atributo Código se administran ahora de manera diferente. Anteriormente, para generar valores para el atributo de código, se usaba el **atributo predeterminado para una acción de valor generado** en el área funcional de **Administración del sistema** en **reglas de negocios**. Ahora, en **Administración del sistema**, debe editar la entidad para habilitar los valores de código generados automáticamente. Para obtener más información, consulte [Creación automática de código &#40;Master Data Services&#41;](automatic-code-creation-master-data-services.md).  
  
 Si tiene un paquete de implementación de modelo de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] que contenga una regla de este tipo, al actualizar la base de datos a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] se excluirá la regla de negocios.  
  
### <a name="bulk-updates-and-exporting"></a>Actualizaciones y exportación masivas  
 En la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], ya no se pueden actualizar los valores de atributo para varios miembros de forma masiva. Para realizar actualizaciones masivas, utilice el proceso de almacenamiento provisional [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]o el.  
  
 En la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], ya no se pueden exportar miembros a Excel. Para trabajar con miembros en Excel, use [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
### <a name="transactions"></a>Transacciones  
 En el área funcional del **Explorador** , los usuarios ya no pueden revertir sus propias transacciones. Anteriormente, los usuarios podían revertir los cambios realizados en los datos en el **Explorador**. Los administradores todavía pueden revertir las transacciones para todos los usuarios en el área funcional de **Administración de versiones** .  
  
 Ahora las anotaciones son permanentes y no se pueden eliminar. Anteriormente, las anotaciones se consideraban transacciones y podían eliminarse invirtiendo la transacción.  
  
### <a name="web-service"></a>Servicio web  
 Ahora el servicio web de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] se habilita automáticamente, tal como requiere Silverlight. Anteriormente, el servicio web tenía que habilitarse manualmente.  
  
### <a name="powershell-cmdlets"></a>Cmdlets de PowerShell  
 MDS ya no incluye los cmdlets de PowerShell.  
  
## <a name="see-also"></a>Consulte también  
 [Características desusadas de Master Data Services en SQL Server 2014](deprecated-master-data-services-features.md)  
  
  
