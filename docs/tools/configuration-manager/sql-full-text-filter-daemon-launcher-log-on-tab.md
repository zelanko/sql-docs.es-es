---
title: "Selector del demonio de filtro de texto completo de SQL (pesta&#241;a Iniciar sesi&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 13e260f9-a75f-430b-88a3-959ddcead8fe
caps.latest.revision: 9
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 9
---
# Selector del demonio de filtro de texto completo de SQL (pesta&#241;a Iniciar sesi&#243;n)
  Desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], la búsqueda de texto completo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el servicio Selector de demonio de filtro de texto completo de SQL (iniciador FDHOST). Este servicio debe estar ejecutándose si se utiliza la búsqueda de texto completo. Para obtener información sobre los procesos de host de demonio de filtro, vea "Arquitectura de la búsqueda de texto completo" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Utilice la **iniciar sesión** ficha de la **Propiedades de selector de demonio de filtro de texto completo SQL** cuadro de diálogo para especificar la cuenta utilizada por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio de búsqueda de texto completo, cambiar la contraseña de una cuenta y para iniciar y detener el servicio. El cambio de la contraseña de una cuenta surte efecto después de reiniciar el servicio.  
  
> [!NOTE]  
>  Cuando cambie el nombre de cuenta utilizado por un servicio en una instancia en clúster, la nueva cuenta debe formar parte del grupo de dominios que haya especificado durante la instalación del servicio, o bien debe tener permiso para agregar miembros a ese grupo. Si no tiene permisos para modificar la pertenencia al grupo, póngase en contacto con el administrador del dominio.  
>   
>  Para obtener información acerca de cómo seleccionar una cuenta para ejecutar el servicio, vea el tema sobre la configuración de cuentas de servicios de Windows en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## Opciones  
 **Cuenta integrada**  
 **Sistema local**  
 Especifique la cuenta de sistema local. Esta cuenta no requiere ninguna contraseña. No obstante, la cuenta del sistema local puede impedir la interacción del servicio con otros servidores, en función de los privilegios que se hayan concedido a la cuenta.  
  
 **Servicio local**  
 Especifique la cuenta de servicio local. Esta cuenta no requiere ninguna contraseña. No obstante, la cuenta de servicio local puede impedir la interacción del servicio con otros servidores, en función de los privilegios que se hayan concedido a la cuenta.  
  
 **Servicio de red**  
 Se recomienda que no utilice la cuenta de servicio de red para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicios o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Servicios del agente. Las cuentas de usuario local o de usuario de dominio son más adecuadas para estos servicios.  
  
 **Esta cuenta**  
 Especifique una cuenta de usuario local o de dominio que utilice la autenticación de Windows. Se recomienda utilizar una cuenta de usuario de dominio que tenga derechos mínimos para los servicios.  
  
 **Nombre de cuenta**  
 Escriba el nombre de la cuenta de usuario local o de dominio.  
  
 **Contraseña**  
 Escriba la contraseña de la cuenta.  
  
 **Confirmar contraseña**  
 Escriba de nuevo la contraseña de la cuenta.  
  
 **Iniciar**  
 Inicie el servicio.  
  
 **Detener**  
 Detenga el servicio.  
  
 **Pausar**  
 Pause el servicio. No disponible para este servicio.  
  
 **Reanudar**  
 Reanude un servicio en pausa.  
  
  