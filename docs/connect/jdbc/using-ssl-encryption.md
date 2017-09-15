---
title: "Está utilizando cifrado SSL | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7923995b392dff8c80f1ee6ae3946e421dc46331
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
|[Configuración del cliente para el cifrado SSL](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md)|Describe cómo configurar el almacén de confianza predeterminado del lado cliente y cómo importar un certificado privado al almacén de confianza del equipo cliente.|  
  
## <a name="see-also"></a>Vea también  
 [Proteger aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
  
  
