---
title: Propiedades del servidor (página Conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.connections.f1
ms.assetid: 33be8ac5-12dd-4b8a-99e0-68261c219dd2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fd6e2883714c538bff1e2ff2a93ace7b71fd5d02
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604195"
---
# <a name="server-properties---connections-page"></a>Propiedades del servidor (página Conexiones)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice esta página para ver o modificar sus opciones de conexión.  
  
## <a name="connections"></a>Conexiones  
 **Número máximo de conexiones simultáneas (0 = ilimitado)**  
 Si se establece en un valor distinto de cero, limita el número de conexiones que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permitirá que se establezcan.  
  
> [!CAUTION]  
>  Si se establece en un valor pequeño, como 1 o 2, es posible que impida a los administradores conectarse para administrar el servidor; sin embargo, la conexión de administrador dedicada podrá conectarse siempre.  
  
## <a name="default-connection-options"></a>Opciones predeterminadas de conexión  
 **Default connection options**  
 Especifica las opciones de conexión predeterminadas, tal y como se describen en la siguiente tabla.  
  
|Opción de configuración|Descripción|  
|--------------------------|-----------------|  
|**disable deferred constraint checking**|Controla la comprobación de restricciones provisionales o diferidas.|  
|**transacciones implícitas**|Controla si una transacción se inicia de manera implícita al ejecutar una instrucción.|  
|**cursor close on commit**|Controla el comportamiento de los cursores después de realizarse una operación de confirmación.|  
|**ansi warnings**|Controla el truncamiento y los valores NULL en las advertencias de agregados.|  
|**ansi padding**|Controla los valores de relleno de las variables de longitud fija.|  
|**ansi nulls**|Controla el tratamiento de los valores `NULL` cuando se utilizan operadores de igualdad.|  
|**arithmetic abort**|Cancela una consulta cuando se produce un error de desbordamiento o división por cero durante su ejecución.|  
|**arithmetic ignore**|Devuelve un valor NULL cuando se produce un error de desbordamiento o de división por cero durante una consulta.|  
|**quoted identifier**|Diferencia entre las comillas simples o dobles al evaluar una expresión.|  
|**no count**|Desactiva el mensaje que se devuelve al final de cada instrucción, que indica el número de filas afectadas.|  
|**ansi null default on**|Altera el comportamiento de la sesión para que utilice la compatibilidad con ANSI para la nulabilidad. Se permite la nulabilidad para las nuevas columnas definidas sin la aceptación explícita de estos valores.|  
|**ansi null default off**|Altera el comportamiento de la sesión para que no utilice la compatibilidad con ANSI para la nulabilidad. Se definen nuevas columnas definidas sin la nulabilidad explícita para permitir valores nulos.|  
|**concat null yields null**|Devuelve un valor NULL al concatenar un valor NULL con una cadena.|  
|**numeric round abort**|Genera un error cuando se produce una pérdida de precisión en una expresión.|  
|**xact abort**|Revierte una transacción si una instrucción Transact- SQL produce un error en tiempo de ejecución.|  
  
 Para obtener más información sobre las opciones de conexión, busque cada opción específica en los Libros en pantalla.  
  
## <a name="remote-server-connections"></a>Conexiones a servidores remotos  
 **Permitir conexiones remotas con este servidor**  
 Controla la ejecución de procedimientos almacenados desde servidores remotos que ejecutan instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La activación de esta casilla tiene el mismo efecto que establecer la opción **sp_configureremote access** en 1. Al desactivarla, se impide la ejecución de procedimientos almacenados desde un servidor remoto.  
  
 **Tiempo de espera de consulta remota (en segundos, 0 = sin tiempo de espera)**  
 Especifica cuánto puede durar (en segundos) una operación remota antes de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supere el tiempo de espera. El valor predeterminado es 600 segundos o una espera de 10 minutos.  
  
 **Exigir transacciones distribuidas para comunicación entre servidores**  
 Protege las acciones de un procedimiento entre servidores a través de un Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC). Para más información, consulte [Establecer la opción de configuración del servidor Transacciones de procedimientos remotos](../../database-engine/configure-windows/configure-the-remote-proc-trans-server-configuration-option.md).  
  
## <a name="property-page-display-options"></a>Opciones de visualización de la página de propiedades  
 **Valores configurados**  
 Muestra los valores configurados para las opciones de este panel. Si cambia estos valores, haga clic en **Valores actuales** para comprobar si los cambios han surtido efecto. Si no tienen, deberá reiniciarse primero la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Valores actuales**  
 Presenta los valores actuales de las opciones de este panel. Estos valores son de solo lectura.  
  
## <a name="see-also"></a>Ver también  
 [Opciones &#40;Ejecución de la consulta/SQL Server/página Avanzadas&#41;](https://msdn.microsoft.com/library/3ec788c7-22c3-4216-9ad0-81a168d17074)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
