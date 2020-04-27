---
title: Establecer la opción de configuración del servidor Idioma de texto completo predeterminado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- default full-text language option
ms.assetid: 0fa8785b-0830-4a52-aff5-fcf8268b72fc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d98194f5dead58b738c39503445923d9df49be06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62787071"
---
# <a name="configure-the-default-full-text-language-server-configuration-option"></a>Establecer la opción de configuración del servidor Idioma de texto completo predeterminado
  En este tema se describe cómo configurar `default full-text language` la opción de configuración [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del servidor [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en [!INCLUDE[tsql](../../includes/tsql-md.md)]mediante o. La `default full-text language` opción especifica un valor de idioma predeterminado para los índices de texto completo. Los análisis lingüísticos se realizan en todos los datos que tienen índices de texto completo y que dependen del idioma de los datos. El valor predeterminado de esta opción es el idioma del servidor. En el caso de una versión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]localizada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , `default full-text language` el programa de instalación de establece la opción en el idioma del servidor si existe una coincidencia adecuada. En las versiones no traducidas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la opción `default full-text language` es el inglés.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de idioma de texto completo predeterminado, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción de idioma de texto completo predeterminado](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El valor de la `default full-text language` opción se usa en un índice de texto completo cuando no se especifica ningún idioma para una columna a través de la opción Language **language_term** en las instrucciones CREATE FULLTEXT INDEX o ALTER fulltext index. Si el idioma predeterminado para búsqueda de texto completo no es compatible o el paquete de análisis lingüístico no está disponible, la operación CREATE o ALTER no será satisfactoria y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devolverá un mensaje de error que indica que el idioma especificado no es válido.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada.  
  
-   La `default full-text language` opción requiere un valor LCID. Para obtener una lista de los LCID admitidos y sus respectivos idiomas, vea [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql). Por ejemplo, es posible que haya otros idiomas disponibles de fabricantes independientes de software. Si no se detecta ningún dialecto de idioma específico, el motor de texto completo cambiará automáticamente al idioma principal.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>Para configurar la opción de idioma de texto completo predeterminado  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y seleccione **Propiedades**.  
  
2.  Haga clic en el nodo **Avanzado** .  
  
3.  En Varios, use la opción **Idioma de texto completo predeterminado** para especificar un valor de idioma predeterminado para las columnas indexadas de texto completo.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>Para configurar la opción de idioma de texto completo predeterminado  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo muestra cómo usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para establecer el valor de la opción de `default full-text` en Neerlandés (`1043`).  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'default full-text language', 1043 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="follow-up-after-you-configure-the-default-full-text-language-option"></a><a name="FollowUp"></a> Seguimiento: Después de configurar la opción de idioma de texto completo predeterminado  
 La configuración surte efecto inmediatamente, sin necesidad de reiniciar el servidor.  
  
## <a name="see-also"></a>Consulte también  
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
