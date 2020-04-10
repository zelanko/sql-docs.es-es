---
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
ms.openlocfilehash: 84499024a5e4dbd158c54624a4ae1c03af9832b1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922388"
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
  
 Es **true** si el cifrado de Capa de sockets seguros (SSL) está habilitado entre el cliente y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Observaciones  
 Si la propiedad encrypt se establece en **true**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] procura que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use el cifrado SSL en todos los datos que se envíen entre el cliente y el servidor, si el servidor tiene un certificado instalado. El valor predeterminado es **false**.  
  
 El controlador JDBC detecta la máquina virtual Java (JVM) que se está ejecutando cuando se intenta establecer un protocolo de enlace SSL.  
  
 Si la propiedad encrypt se establece en **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usa el proveedor de seguridad JSSE predeterminado de JVM para negociar el cifrado SSL con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El proveedor de seguridad predeterminado puede no admitir todas las características necesarias para negociar el cifrado SSL correctamente. Por ejemplo, es posible que el proveedor de seguridad predeterminado no admita el tamaño de la clave pública RSA que se usa en el certificado SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. En este caso, el proveedor de seguridad predeterminado podría generar un error que ocasionará que el controlador JDBC termine la conexión. Para resolver este problema, intente una de las siguientes acciones:  
  
-   Configurar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con un certificado de servidor que tenga una clave pública RSA más pequeña  
  
-   Configurar la JVM para usar un proveedor de seguridad JSSE diferente en el archivo de propiedades de seguridad "\<java-home>/lib/security/java.security"  
  
-   Usar una JVM distinta  
  
 Si la propiedad de cifrado no se ha especificado o se ha establecido en **false**, el controlador no aplicará [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para admitir el cifrado SSL. Si la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se configura para exigir el cifrado SSL, se establece una conexión sin cifrado. Si la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está configurada para exigir el cifrado SSL, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] habilitará automáticamente el cifrado SSL cuando se ejecute en una máquina virtual Java (JVM) configurada correctamente; de lo contrario, se finalizará la conexión y el controlador generará un error.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
