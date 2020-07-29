---
title: Uso de cifrado
ms.custom: Learn how to establish secure communication channels using TLS encryption with your SQL database connections.
ms.date: 09/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: vanto
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8e566243-2f93-4b21-8065-3c8336649309
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1d55189e01bbc68772163bcd054165737ae186ee
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2020
ms.locfileid: "86391820"
---
# <a name="using-encryption"></a>Uso de cifrado

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

La seguridad de la capa de transporte (TLS) habilita la transmisión de datos cifrados a través de la red entre una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y una aplicación cliente.  
  
La seguridad de la capa de transporte (TLS) es un protocolo para establecer un canal de comunicaciones seguro para evitar la interceptación de información esencial o confidencial por la red y otras comunicaciones de Internet. TLS permite al cliente y al servidor autenticar la identidad de cada uno. Después de autenticar a los participantes, TLS proporciona conexiones cifradas entre ellos para proteger la transmisión de los mensajes.  
  
El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] proporciona una infraestructura para habilitar y deshabilitar el cifrado en una conexión determinada según las propiedades de conexión especificadas por el usuario y la configuración del cliente y el servidor. El usuario puede especificar la ubicación del almacén de certificados y la contraseña, un nombre de host que se va a utilizar para validar el certificado y cuándo cifrar el canal de comunicaciones.  
  
Al habilitar el cifrado TLS aumenta la seguridad de los datos que se transmiten a través de redes entre instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las aplicaciones. No obstante, también reduce el rendimiento.  
  
En los temas de esta sección se describe cómo la versión del [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el cifrado TLS, incluidas las nuevas propiedades de conexión, y cómo se puede configurar el almacén de confianza en el lado cliente.  
  
> [!NOTE]  
> Se recomienda usar la propiedad de conexión **hostNameInCertificate** para validar un certificado TLS.  

## <a name="in-this-section"></a>En esta sección  

| Tema                                                                                                        | Descripción                                                                                                                                           |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Descripción de la compatibilidad con cifrado](../../connect/jdbc/understanding-ssl-support.md)                                 | Describe cómo el [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el cifrado TLS.                                              |
| [Conexión con cifrado](../../connect/jdbc/connecting-with-ssl-encryption.md)                       | Describe cómo conectarse a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con las nuevas propiedades de conexión específicas de TLS. |
| [Configuración del cliente para el cifrado](../../connect/jdbc/configuring-the-client-for-ssl-encryption.md) | Describe cómo configurar el almacén de confianza predeterminado del lado cliente y cómo importar un certificado privado al almacén de confianza del equipo cliente.   |
  
## <a name="see-also"></a>Consulte también

[Protección de las aplicaciones del controlador JDBC](../../connect/jdbc/securing-jdbc-driver-applications.md)  
