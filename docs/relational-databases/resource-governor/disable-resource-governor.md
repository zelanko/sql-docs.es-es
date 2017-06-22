---
title: Deshabilitar el regulador de recursos | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, disabling
ms.assetid: 2c2d2db0-34a5-4f50-b783-17693e3ce3f1
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 47091df9ec1318e7bb66ef1a32346c7445b4abd6
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="disable-resource-governor"></a>Deshabilitar el regulador de recursos
  Puede deshabilitar el regulador de recursos utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o Transact-SQL.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To disable Resource Governorn, using:**  [Object Explorer](#RGOffObjEx), [Resource Governor Properties](#RGOffProp), [Transact-SQL](#RGOffTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 Deshabilitar el regulador de recursos tiene como consecuencia lo siguiente:  
  
-   No se ejecuta la función clasificadora.  
  
-   Todas las conexiones nuevas se clasifican automáticamente en el grupo de carga de trabajo predeterminado.  
  
-   Las solicitudes iniciadas por el sistema se clasifican en el grupo de cargas de trabajo interno.  
  
-   Se restablecen los valores predeterminados de todas las configuraciones existentes del grupo de cargas de trabajo y el grupo de recursos de servidor. En este caso, no se desencadena ningún evento cuando se alcanzan los límites.  
  
-   La supervisión normal del sistema no resulta afectada.  
  
-   Se puede cambiar la configuración, pero los cambios no surtirán efecto hasta que se habilite el regulador de recursos.  
  
-   Al reiniciar SQL Server, el regulador de recursos no cargará su configuración, sino que tendrá únicamente los grupos de cargas de trabajo y los grupos de recursos de servidor predeterminados e internos.  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 No puede utilizar la instrucción **ALTER RESOURCE GOVERNOR** para deshabilitar el regulador de recursos durante una transacción del usuario.  
  
###  <a name="Permissions"></a> Permisos  
 Deshabilitar el regulador de recursos requiere el permiso CONTROL SERVER.  
  
##  <a name="RGOffObjEx"></a> Deshabilitar el regulador de recursos mediante el Explorador de objetos  
 **Para deshabilitar el regulador de recursos utilizando el Explorador de objetos**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos y expanda de forma recursiva el nodo **Administración** hasta el nodo **Regulador de recursos**.  
  
2.  Haga clic con el botón derecho en **Regulador de recursos**y, luego, haga clic en **Deshabilitar**.  
  
##  <a name="RGOffProp"></a> Deshabilitar el regulador de recursos mediante Propiedades del regulador de recursos  
 **Para deshabilitar el regulador de recursos mediante la página Propiedades del regulador de recursos**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos y expanda de forma recursiva el nodo **Administración** hasta el nodo **Regulador de recursos**.  
  
2.  Haga clic con el botón derecho en **Regulador de recursos** y, luego, haga clic en **Propiedades**. De este modo se abre la página **Propiedades del regulador de recursos** .  
  
3.  Haga clic en la casilla **Habilitar regulador de recursos** , asegúrese de que la casilla no está activada, y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="RGOffTSQL"></a> Deshabilitar el regulador de recursos mediante Transact-SQL  
 **Para deshabilitar el regulador de recursos mediante Transact-SQL**  
  
1.  Ejecute la instrucción **ALTER RESOURCE GOVERNOR DISABLE** .  
  
### <a name="example-transact-sql"></a>Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se habilita el regulador de recursos.  
  
```  
ALTER RESOURCE GOVERNOR DISABLE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar el regulador de recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Grupos de cargas de trabajo del regulador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Función clasificadora del regulador de recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
