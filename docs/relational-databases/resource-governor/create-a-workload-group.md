---
title: Creación de un grupo de cargas de trabajo | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: resource-governor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
ms.assetid: 072868ec-ceff-4db6-941b-281af731a067
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 957dee75abdbe09455972bc28fc89a40af892a0f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-workload-group"></a>Crear un grupo de cargas de trabajo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Puede crear un grupo de cargas de trabajo utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de empezar:**  [Limitaciones y restricciones](#LimitationsRestrictions), [Permisos](#Permissions)  
  
-   **Para crear un grupo de cargas de trabajo, utilice:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 La memoria consumida por la creación de índices en una tabla con particiones no alineada es proporcional al número de particiones involucradas. Si la memoria total necesaria supera el límite por consulta (REQUEST_MAX_MEMORY_GRANT_PERCENT) impuesto por la configuración del grupo de cargas de trabajo, puede que esta creación de índices produzca un error. Dado que el grupo de cargas de trabajo predeterminado permite que una consulta supere el límite por consulta con la memoria mínima necesaria para iniciar la compatibilidad con SQL Server 2005, es posible que el usuario pueda ejecutar la misma creación de índices en el grupo de cargas de trabajo predeterminado si el grupo de recursos de servidor predeterminado tiene configurada una memoria total suficiente para ejecutar una consulta.  
  
 Se permite la creación de índices para usar más memoria del área de trabajo que la concedida inicialmente para mejorar el rendimiento. El regulador de recursos admite este tratamiento especial; sin embargo, la concesión inicial y cualquier concesión de memoria adicional están limitadas por la configuración del grupo de cargas de trabajo y el grupo de recursos de servidor.  
  
###  <a name="Permissions"></a> Permissions  
 Crear un grupo de cargas de trabajo requiere un permiso CONTROL SERVER.  
  
##  <a name="CreRPProp"></a> Crear un grupo de cargas de trabajo mediante SQL Server Management Studio  
 **Para crear un grupo de cargas de trabajo utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  En el Explorador de objetos, expanda de forma recursiva el nodo **Administración** hasta e incluyendo el grupo de recursos de servidor que contiene el grupo de cargas de trabajo que va a modificar.  
  
2.  Haga clic con el botón derecho en la carpeta **Grupos de cargas de trabajo** y luego haga clic en **Nuevo grupo de cargas de trabajo**.  
  
3.  En la cuadrícula **Grupos de recursos** , asegúrese de que está resaltado el grupo de recursos de servidor al que desea agregar el grupo de carga de trabajo.  
  
4.  La cuadrícula **Grupos de cargas de trabajo de grupo de recursos de servidor** tendrá una nueva línea con un nombre en blanco y los valores predeterminados en las otras columnas.  
  
5.  Haga clic en la celda **Nombre** y escriba un nombre para el grupo de cargas de trabajo.  
  
6.  Haga clic o doble clic en cualquier otra celda de la fila cuya configuración predeterminada desee cambiar, y especifique los nuevos valores.  
  
7.  Haga clic en **Aceptar**para guardar los cambios.  
  
##  <a name="CreRPTSQL"></a> Crear un grupo de cargas de trabajo mediante Transact-SQL  
 **Para crear un grupo de cargas de trabajo utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Ejecute la instrucción CREATE WORKLOAD GROUP especificando los valores de propiedad que desea establecer.  
  
2.  Ejecute la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
### <a name="example-transact-sql"></a>Ejemplo (Transact-SQL)  
 El siguiente ejemplo crea un grupo de cargas de trabajo denominado `groupAdhoc` en el grupo de recursos de servidor denominado `poolAdhoc`.  
  
```  
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar el regulador de recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Crear un grupo de recursos de servidor](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Cambiar la configuración del grupo de cargas de trabajo](../../relational-databases/resource-governor/change-workload-group-settings.md)   
 [Crear y probar una función clasificadora definida por el usuario](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
  
