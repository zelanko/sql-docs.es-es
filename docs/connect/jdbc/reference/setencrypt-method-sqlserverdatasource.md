---
description: Método setEncrypt (SQLServerDataSource)
title: Método setEncrypt (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setEncrypt Method (SQLServerDataSource)
apilocation:
- setEncrypt Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 0c85a9c1-f27c-457e-8461-403cc03e2d17
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e7da98aa70be2066c370b75e2bc213c25ba16e03
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431977"
---
# <a name="setencrypt-method-sqlserverdatasource"></a>Método setEncrypt (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un valor **Boolean** que indica si la propiedad encrypt está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setEncypt(boolean encrypt)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *encrypt*  
  
 Es **true** si el cifrado de Seguridad de la capa de transporte (TLS), antes conocida como Capa de sockets seguros (SSL), está habilitado entre el cliente y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Observaciones  
 Si la propiedad encrypt se establece en **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se asegura de que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el cifrado TLS en todos los datos que se envíen entre el cliente y el servidor, si el servidor tiene un certificado instalado. El valor predeterminado es **false**.  
  
 El controlador JDBC detecta la máquina virtual Java (JVM) que se está ejecutando cuando se intenta establecer un protocolo de enlace TLS.  
  
 Si la propiedad encrypt se establece en **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usa el proveedor de seguridad JSSE predeterminado de JVM para negociar el cifrado TLS con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El proveedor de seguridad predeterminado puede no admitir todas las características necesarias para negociar el cifrado TLS correctamente. Por ejemplo, es posible que el proveedor de seguridad predeterminado no admita el tamaño de la clave pública RSA que se usa en el certificado TLS/SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. En este caso, el proveedor de seguridad predeterminado podría generar un error que ocasionará que el controlador JDBC termine la conexión. Para resolver este problema, intente una de las siguientes acciones:  
  
-   Configurar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con un certificado de servidor que tenga una clave pública RSA más pequeña  
  
-   Configurar la JVM para usar otro proveedor de seguridad JSSE en el archivo de propiedades de seguridad "\<java-home>/lib/security/java.security"  
  
-   Usar una JVM distinta  
  
 Si la propiedad encrypt no se ha especificado o se ha establecido en **false**, el controlador no aplicará [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para admitir el cifrado TLS. Si la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se configura para exigir el cifrado TLS, se establece una conexión sin cifrado. Si la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está configurada para exigir el cifrado TLS, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] habilitará automáticamente el cifrado TLS cuando se ejecute en una máquina virtual Java (JVM) configurada correctamente; de lo contrario, se finalizará la conexión y el controlador generará un error.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
