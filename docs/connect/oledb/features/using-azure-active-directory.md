---
title: Usar Azure Active Directory | Microsoft Docs para SQL Server
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: b459877be731da11b33d13772bbf186ecf72198c
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381850"
---
# <a name="using-azure-active-directory"></a>Uso de Azure Active Directory
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="purpose"></a>Finalidad

A partir de la versión 18.2.1, Microsoft OLE DB driver for SQL Server permite que OLE DB aplicaciones se conecten a una instancia de Azure SQL Database mediante una identidad federada. Los nuevos métodos de autenticación incluyen:
- IDENTIFICADOR de inicio de sesión de Azure Active Directory y contraseña
- Token de acceso de Azure Active Directory
- Autenticación integrada de Azure Active Directory
- IDENTIFICADOR y contraseña de inicio de sesión de SQL

La versión 18,3 agrega compatibilidad para los siguientes métodos de autenticación:
- Autenticación interactiva de Azure Active Directory
- Autenticación MSI de Azure Active Directory

> [!NOTE]
> No se admite el uso de `DataTypeCompatibility` los siguientes modos de autenticación con (o `80` su propiedad correspondiente) establecer en **no** es compatible
> - Azure Active Directory la autenticación mediante el identificador de inicio de sesión y la contraseña
> - Autenticación Azure Active Directory mediante el token de acceso
> - Autenticación integrada de Azure Active Directory
> - Autenticación interactiva de Azure Active Directory
> - Autenticación MSI de Azure Active Directory

## <a name="connection-string-keywords-and-properties"></a>Palabras clave y propiedades de cadena de conexión
Se han introducido las siguientes palabras clave de cadena de conexión para admitir la autenticación Azure Active Directory:

|Palabra clave de cadena de conexión|Propiedad Conexión|Descripción|
|---               |---                |---        |
|Token de acceso|SSPROP_AUTH_ACCESS_TOKEN|Especifica un token de acceso para autenticarse en Azure Active Directory. |
|Autenticación|SSPROP_AUTH_MODE|Especifica el método de autenticación que se va a utilizar.|

Para obtener más información acerca de las nuevas palabras clave y propiedades, vea las siguientes páginas:
- [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)
- [Propiedades de inicialización y autorización](../ole-db-data-source-objects/initialization-and-authorization-properties.md)

## <a name="encryption-and-certificate-validation"></a>Cifrado y validación de certificados
En esta sección se describen los cambios en el comportamiento de cifrado y validación de certificados. Estos cambios **solo** se aplican cuando se usan las nuevas palabras clave de cadena de conexión de autenticación o token de acceso (o sus propiedades correspondientes).

### <a name="encryption"></a>Cifrado
Para mejorar la seguridad, cuando se usan las nuevas propiedades/palabras clave de conexión, el controlador invalida el valor de cifrado predeterminado estableciéndolo en `yes`. La invalidación se produce en el tiempo de inicialización del objeto de origen de datos. Si el cifrado se establece antes de la inicialización por cualquier medio, el valor se respeta y no se reemplaza.

> [!NOTE]   
> En las aplicaciones ADO y en las aplicaciones que obtienen la interfaz `IDBInitialize` a través de `IDataInitialize::GetDataSource`, el componente principal que implementa la interfaz establece explícitamente el cifrado en su valor predeterminado de `no`. Como resultado, las nuevas propiedades o palabras clave de autenticación respetan esta configuración y el valor de cifrado **no** se reemplazan. Por lo tanto, se **recomienda** que estas aplicaciones establezcan explícitamente `Use Encryption for Data=true` para reemplazar el valor predeterminado.

### <a name="certificate-validation"></a>Validación de certificados
Para mejorar la seguridad, las nuevas palabras clave y propiedades de conexión respetan el valor de `TrustServerCertificate` (y sus correspondientes palabras clave y propiedades de cadena de conexión) **independientemente de la configuración de cifrado de cliente**. Como resultado, se valida el certificado de servidor de forma predeterminada.

> [!NOTE]   
> La validación del certificado también se puede controlar a través del campo `Value` de la entrada del registro `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SNI18.0\GeneralFlags\Flag2`. Los valores válidos son `0` y `1`. El controlador de OLE DB elige la opción más segura entre el registro y la configuración de la propiedad de conexión/palabra clave. Es decir, el controlador validará el certificado de servidor siempre y cuando al menos una de las opciones de registro o conexión habilite la validación de certificados de servidor.

## <a name="gui-additions"></a>Adiciones de GUI
La interfaz gráfica de usuario del controlador se ha mejorado para permitir la autenticación Azure Active Directory. Para obtener más información, vea:
- [Cuadro de diálogo de inicio de sesión de SQL Server](../help-topics/sql-server-login-dialog.md)
- [Configuración de vínculo de datos universal (UDL)](../help-topics/data-link-pages.md)

## <a name="example-connection-strings"></a>Ejemplos de cadena de conexión
En esta sección se muestran ejemplos de palabras clave de cadena de conexión nuevas y existentes que se van a utilizar con `IDataInitialize::GetDataSource` y `DBPROP_INIT_PROVIDERSTRING` propiedad.

### <a name="sql-authentication"></a>Autenticación SQL
- Usar `IDataInitialize::GetDataSource`:
    - Nuevo:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=SqlPassword**;User ID=[username];Password=[password];Use Encryption for Data=true
    - Obsoleto:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];User ID=[username];Password=[password];Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    - Nuevo:
        > Server=[server];Database=[database];**Authentication=SqlPassword**;UID=[username];PWD=[password];Encrypt=yes
    - Obsoleto:
        > Server=[server];Database=[database];UID=[username];PWD=[password];Encrypt=yes

### <a name="integrated-windows-authentication-using-security-support-provider-interface-sspi"></a>Autenticación integrada de Windows mediante la interfaz del proveedor de compatibilidad para seguridad (SSPI)

- Usar `IDataInitialize::GetDataSource`:
    - Nuevo:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
    - Obsoleto:
        > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Integrated Security=SSPI**;Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    - Nuevo:
        > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes
    - Obsoleto:
        > Server=[server];Database=[database];**Trusted_Connection=yes**;Encrypt=yes

### <a name="azure-active-directory-username-and-password-authentication"></a>Azure Active Directory la autenticación de nombre de usuario y contraseña

- Usar `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryPassword**;User ID=[username];Password=[password];Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryPassword**;UID=[username];PWD=[password];Encrypt=yes

### <a name="azure-active-directory-integrated-authentication"></a>Autenticación integrada de Azure Active Directory

- Usar `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[server];Initial Catalog=[database];**Authentication=ActiveDirectoryIntegrated**;Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    > Server=[server];Database=[database];**Authentication=ActiveDirectoryIntegrated**;Encrypt=yes

### <a name="azure-active-directory-authentication-using-an-access-token"></a>Azure Active Directory la autenticación mediante un token de acceso

- Usar `IDataInitialize::GetDataSource`:
    > Provider = MSOLEDBSQL; Data Source = [Server]; Initial Catalog = [base de datos]; **Token de acceso = [token de acceso]** ; Usar cifrado para datos = true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    > No se admite proporcionar el token de acceso a través de `DBPROP_INIT_PROVIDERSTRING`

### <a name="azure-active-directory-interactive-authentication"></a>Autenticación interactiva de Azure Active Directory

- Usar `IDataInitialize::GetDataSource`:
    > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[base de datos];**Authentication=ActiveDirectoryInteractive**;User ID=[nombre de usuario];Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    > Server = [Server];D ase = [base de datos]; **Autenticación = ActiveDirectoryInteractive**; UID = [nombre de usuario]; Cifrar = sí

### <a name="azure-active-directory-msi-authentication"></a>Autenticación MSI de Azure Active Directory

- Usar `IDataInitialize::GetDataSource`:
    - Identidad administrada asignada por el usuario:
        > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[base de datos];**Authentication=ActiveDirectoryMSI**;User ID=[Id. de objeto];Use Encryption for Data=true
    - Identidad administrada asignada por el sistema:
        > Provider=MSOLEDBSQL;Data Source=[servidor];Initial Catalog=[base de datos];**Authentication=ActiveDirectoryMSI**;Use Encryption for Data=true
- Usar `DBPROP_INIT_PROVIDERSTRING`:
    - Identidad administrada asignada por el usuario:
        > Server = [Server];D ase = [base de datos]; **Autenticación = ActiveDirectoryMSI**; UID = [ID. de objeto]; Cifrar = sí
    - Identidad administrada asignada por el sistema:
        > Server = [Server];D ase = [base de datos]; **Autenticación = ActiveDirectoryMSI**; Cifrar = sí

## <a name="code-samples"></a>Ejemplos de código

En los siguientes ejemplos se muestra el código necesario para conectarse a Azure Active Directory con palabras clave de conexión. 

### <a name="access-token"></a>Token de acceso
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    wchar_t accessToken[] = L"eyJ0eXAiOi...";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Access Token=" + accessToken + L";Use Encryption for Data=true;";
    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```
### <a name="active-directory-integrated"></a>Active Directory Integrated
```cpp
#include <string>
#include <iostream>
#include <msdasc.h>

int main()
{
    wchar_t azureServer[] = L"server";
    wchar_t azureDatabase[] = L"mydatabase";
    IDBInitialize *pIDBInitialize = nullptr;
    IDataInitialize* pIDataInitialize = nullptr;
    HRESULT hr = S_OK;

    CoInitialize(nullptr);

    // Construct the connection string.
    std::wstring connString = L"Provider=MSOLEDBSQL;Data Source=" + std::wstring(azureServer) + L";Initial Catalog=" + 
                              std::wstring(azureDatabase) + L";Authentication=ActiveDirectoryIntegrated;Use Encryption for Data=true;";

    hr = CoCreateInstance(CLSID_MSDAINITIALIZE, nullptr, CLSCTX_INPROC_SERVER, 
                          IID_IDataInitialize, reinterpret_cast<LPVOID*>(&pIDataInitialize));
    if (FAILED(hr)) 
    {
        std::cout << "Failed to create an IDataInitialize instance." << std::endl;
        goto Cleanup;
    }
    hr = pIDataInitialize->GetDataSource(nullptr, CLSCTX_INPROC_SERVER, connString.c_str(), 
                                         IID_IDBInitialize, reinterpret_cast<IUnknown**>(&pIDBInitialize));
    if (FAILED(hr))
    {
        std::cout << "Failed to get data source object." << std::endl;
        goto Cleanup;
    }
    hr = pIDBInitialize->Initialize();
    if (FAILED(hr))
    {
        std::cout << "Failed to establish connection." << std::endl;
        goto Cleanup;
    }

Cleanup:
    if (pIDBInitialize)
    {
        pIDBInitialize->Uninitialize();
        pIDBInitialize->Release();
    }
    if (pIDataInitialize)
    {
        pIDataInitialize->Release();
    }

    CoUninitialize();
}
```

## <a name="next-steps"></a>Pasos siguientes
- [Autorice el acceso a Azure Active Directory aplicaciones web mediante el flujo de concesión de código de OAuth 2,0](https://go.microsoft.com/fwlink/?linkid=2072672).

- Aprenda más sobre la [autenticación de Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=2073783) a SQL Server.

- Configure las conexiones de controlador mediante [palabras clave de cadena de conexión](../applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md) que admite el controlador de OLE DB.
