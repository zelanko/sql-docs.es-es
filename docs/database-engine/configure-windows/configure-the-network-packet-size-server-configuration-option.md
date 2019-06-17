---
title: Establecer la opción de configuración del servidor Tamaño de paquete de red | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default packet size
- size [SQL Server], packets
- packets [SQL Server], size
- network packet size option
ms.assetid: 236985bf-fc4a-4a57-98f7-a71ef977fd7b
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 90cef82fd04294022e6ab41ec07526deb8c438cc
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802483"
---
# <a name="configure-the-network-packet-size-server-configuration-option"></a>Establecer la opción de configuración del servidor Tamaño de paquete de red
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo establecer la opción de configuración del servidor **tamaño de paquete de red** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La opción de **tamaño de paquete de red** establece el tamaño de paquete (en bytes) que se usa para toda la red. Los paquetes son fragmentos de datos de tamaño fijo que transfieren solicitudes y resultados entre clientes y servidores. El tamaño predeterminado de los paquetes es de 4096 bytes.  
  
> [!NOTE]  
>  No cambie el tamaño de los paquetes a menos que esté seguro de que mejorará el rendimiento. En la mayoría de las aplicaciones, el tamaño más conveniente de los paquetes es el tamaño predeterminado.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de tamaño de paquete de red, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción de tamaño de paquete de red](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El tamaño de paquete de red máximo para las conexiones cifradas es de 16.383 bytes.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un profesional certificado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Si una aplicación realiza operaciones de copia masiva, o bien envía o recibe una gran cantidad de datos de texto o imagen, el uso de paquetes de un tamaño superior al predeterminado podría mejorar la eficacia, ya que tiene como resultado un número menor de operaciones de lectura y escritura en la red. Si una aplicación envía y recibe pequeñas cantidades de información, puede establecer un tamaño de 512 bytes para cada paquete, lo que es suficiente para la mayor parte de las transferencias de datos.  
  
-   En sistemas que usen diferentes protocolos de red, establezca el tamaño de paquete de red en el tamaño para el protocolo más usado. La opción network packet size mejora el rendimiento de la red cuando los protocolos de red admiten paquetes más grandes. Las aplicaciones cliente pueden suplantar este valor.  
  
-   También puede llamar a funciones de OLE DB, Conectividad abierta de bases de datos (ODBC) y DB-Library para solicitar un cambio del tamaño de los paquetes. Si el servidor no puede admitir el tamaño del paquete solicitado, [!INCLUDE[ssDE](../../includes/ssde-md.md)] enviará un mensaje de advertencia al cliente. En algunos casos, el cambio del tamaño del paquete podría crear un error del vínculo de comunicación como el siguiente:  
  
     `Native Error: 233, no process is on the other end of the pipe.`  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-configure-the-network-packet-size-option"></a>Para configurar la opción de tamaño de paquete de red  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y seleccione **Propiedades**.  
  
2.  Haga clic en el nodo **Avanzado** .  
  
3.  En **Red**, seleccione un valor para el cuadro **Tamaño de paquete de red** .  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-the-network-packet-size-option"></a>Para configurar la opción de tamaño de paquete de red  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para establecer el valor de la opción de `network packet size` en `6500` bytes.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'network packet size', 6500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Seguimiento: Después de configurar la opción de tamaño de paquete de red  
 La configuración surte efecto inmediatamente, sin necesidad de reiniciar el servidor.  
  
## <a name="see-also"></a>Consulte también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
