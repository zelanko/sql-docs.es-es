---
title: Está utilizando cifrado SSL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5444946843576f87b6887d2bc9446d0a93d5106d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-ssl-encryption"></a>Usar el cifrado SSL
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Cifrado de Secure Sockets Layer (SSL) habilita la transmisión de datos cifrados a través de la red entre una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y una aplicación cliente.  
  
 Capa de sockets seguros (SSL) es un protocolo para establecer un canal de comunicaciones seguro para evitar la interceptación de información esencial o confidencial por la red y otras comunicaciones de Internet. SSL permite al cliente y al servidor autenticar la identidad de cada uno. Después de autenticar a los participantes, SSL proporciona conexiones cifradas entre ellos para proteger la transmisión de los mensajes.  
  
 El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona una infraestructura para habilitar y deshabilitar el cifrado en una conexión determinada según el especificadas por el usuario propiedades de conexión y la configuración de cliente y servidor. El usuario puede especificar la ubicación del almacén de certificados y la contraseña, un nombre de host que se va a utilizar para validar el certificado y cuándo cifrar el canal de comunicaciones.  
  
 Al habilitar el cifrado SSL se aumenta la seguridad de los datos que se transmiten a través de redes entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y aplicaciones. No obstante, también reduce el rendimiento.  
  
 Los temas de esta sección describen cómo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] versión admite el cifrado de SSL, incluidas nuevas propiedades de conexión y cómo se puede configurar el almacén de confianza en el lado del cliente.  
  
> [!NOTE]  
>  El **hostNameInCertificate** propiedad de conexión se recomienda validar un certificado SSL.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Descripción de la compatibilidad con SSL](../../connect/jdbc/understanding-ssl-support.md)|Describe cómo el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el cifrado SSL.|  
|[Conectar con el cifrado SSL](../../connect/jdbc/connecting-with-ssl-encryption.md)|Describe cómo conectarse a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] base de datos mediante las nuevas propiedades de conexión específicas de SSL.|  
|[Configurar el cliente para el cifrado SSL](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)|Describe cómo configurar el almacén de confianza predeterminado del lado cliente y cómo importar un certificado privado al almacén de confianza del equipo cliente.|  
  
## <a name="see-also"></a>Vea también  
 [Proteger las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
