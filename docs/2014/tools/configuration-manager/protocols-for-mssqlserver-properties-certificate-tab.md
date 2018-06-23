---
title: Propiedades de Protocolos de MSSQLSERVER (pestaña Certificado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.computermgr.cert.general.f1
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 776addd6-25f3-4875-9a71-064035787090
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a1ab765e0c03f8e7561658676141a48785b5e843
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203090"
---
# <a name="protocols-for-mssqlserver-properties-certificate-tab"></a>Propiedades de Protocolos de MSSQLSERVER (pestaña Certificado)
  Utilice la pestaña **Certificado** del cuadro de diálogo **Propiedades de Protocolos de MSSQLSERVER** para seleccionar un certificado para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o ver las propiedades de un certificado. Todos los campos están en blanco hasta que se selecciona un certificado.  
  
 Los certificados se almacenan localmente para los usuarios del equipo. Para cargar un certificado que se va a utilizar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe ejecutar el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la misma cuenta de usuario que el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="page-header"></a>Encabezado de página  
 **Ver**  
 Proporciona acceso a detalles adicionales acerca del certificado. No está disponible hasta que se selecciona un certificado en el cuadro **Certificado** . Para obtener información adicional acerca de los detalles del certificado, vea la documentación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Desactivar**  
 Quita la selección del cuadro **Certificado** .  
  
 **Certificado**  
 Nombre del certificado determinado por el proveedor de seguridad. Seleccione un certificado para ver los detalles en la cuadrícula de propiedades.  
  
## <a name="options"></a>Opciones  
 Fecha de expiración  
 Fecha final del período de validez del certificado.  
  
 Nombre descriptivo  
 Nombre descriptivo o común para la persona o entidad de certificación a la que se emite el certificado.  
  
 Emitido por  
 Información relativa a la entidad de certificación que ha emitido el certificado.  
  
 Emitido a  
 Información relativa al destinatario del certificado.  
  
  