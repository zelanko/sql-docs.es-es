---
title: "Configurar un servidor para escuchar en una canalizaci&#243;n alternativa (Administrador de configuraci&#243;n de SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Canalizaciones con nombre [SQL Server], configurar"
  - "escuchar [SQL Server], canalizaciones"
  - "canalizaciones [SQL Server], alternativas"
  - "canalizaciones alternativas [SQL Server]"
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Configurar un servidor para escuchar en una canalizaci&#243;n alternativa (Administrador de configuraci&#243;n de SQL Server)
  En este tema se describe cómo configurar un servidor para que escuche en una canalización alternativa en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. De forma predeterminada, la instancia predeterminada de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escucha en la canalización con nombre \\\\.\pipe\sql\query. Las instancias con nombre de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y [!INCLUDE[ssEW](../../includes/ssew-md.md)] escuchan en otras canalizaciones.  
  
 Hay tres formas de conectarse a una canalización con nombre específica con una aplicación cliente:  
  
-   Ejecutar el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor.  
  
-   Crear un alias en el cliente, especificando la canalización con nombre.  
  
-   Programar el cliente para conectarse mediante una cadena de conexión personalizada.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### Para configurar la canalización con nombre utilizada por el Motor de base de datos de SQL Server  
  
1.  En el panel de la consola del Administrador de configuración de SQL Server, expanda **Configuración de red de SQL Server** y, luego, haga clic en **Protocolos de** *\<nombre de instancia>*.  
  
2.  En el panel de detalles, haga clic con el botón derecho en **Canalizaciones con nombre** y, después, haga clic en **Propiedades**.  
  
3.  En la pestaña **Protocolo** , en el cuadro **Nombre de canalización** , escriba la canalización en la que desea que escuche [!INCLUDE[ssDE](../../includes/ssde-md.md)] y, a continuación, haga clic en **Aceptar**.  
  
4.  En el panel de la consola, haga clic en **Servicios de SQL Server**.  
  
5.  En el panel de detalles, haga clic con el botón derecho en **SQL Server (**\<nombre de instancia>**)** y, después, haga clic en **Reiniciar** para detener y reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escuchando en una canalización alternativa, hay tres formas de conectarse a una canalización con nombre específica con una aplicación cliente:  
  
-   Ejecutar el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor.  
  
-   Crear un alias en el cliente, especificando la canalización con nombre.  
  
-   Programar el cliente para conectarse mediante una cadena de conexión personalizada.  
  
## Vea también  
 [Crear o eliminar un alias de servidor para que lo utilice un cliente &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/create or delete a server alias for use by a client.md)   
 [Configuración de red del servidor](../../database-engine/configure-windows/server-network-configuration.md)  
  
  