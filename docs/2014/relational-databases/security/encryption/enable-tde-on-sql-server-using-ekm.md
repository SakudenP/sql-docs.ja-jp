---
title: EKM を使用して TDE を有効にする |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], TDE using an EKM
- TDE, EKM how to
- EKM, TDE how to
- Transparent Data Encryption, using EKM
ms.assetid: b892e7a7-95bd-4903-bf54-55ce08e225af
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: e659c5ff0245fdb17192b845eafc60badf5e295e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063211"
---
# <a name="enable-tde-using-ekm"></a>EKM を使用して TDE を有効にする
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]の拡張キー管理 (EKM) モジュールに格納されている非対称キーを使用してデータベース暗号化キーを保護する透過的なデータ暗号化 (TDE) を可能にする方法について説明します。  
  
 TDE は、データベース暗号化キーと呼ばれる対称キーを使用してデータベース全体のストレージを暗号化します。 データベース暗号化キーは、master データベースのデータベース マスター キーによって保護される証明書を使用して保護することもできます。 データベース マスター キーを使用してデータベース暗号化キーを保護する方法の詳細については、「[透過的なデータ暗号化 &#40;TDE&#41;](transparent-data-encryption.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] が Azure 仮想マシンで実行されているときに TDE を構成する方法については、「[Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](extensible-key-management-using-azure-key-vault-sql-server.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   [Transact-SQL を使用して、EKM による TDE を可能にするには](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項  
  
-   データベース暗号化キーの作成およびデータベースの暗号化は、高い特権を持つユーザー (システム管理者など) が行う必要があります。 このユーザーは、EKM モジュールが認証できるユーザーである必要があります。  
  
-   [!INCLUDE[ssDE](../../../includes/ssde-md.md)] は、起動時にデータベースを開く必要があります。 これを行うには、EKM によって認証される資格情報を作成し、非対称キーに基づくログインにその資格情報を追加する必要があります。 ユーザーがこのログインを使用してログインすることはできませんが、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] は EKM デバイスで自身を認証することができます。  
  
-   EKM モジュールに格納されている非対称キーが失われている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]はデータベースを開くことができません。 EKM プロバイダーを使用して非対称キーをバックアップできる場合は、バックアップを作成して安全な場所に保存しておく必要があります。  
  
-   EKM プロバイダーによって要求されるオプションとパラメーターは、次のコード例に含まれるものとは異なっている場合があります。 詳細については、EKM プロバイダーを参照してください。  
  
###  <a name="security"></a><a name="Security"></a> セキュリティ  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissions  
 このトピックでは、次の権限を使用します。  
  
-   構成オプションを変更して RECONFIGURE ステートメントを実行するには、ALTER SETTINGS サーバーレベル権限が与えられている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
-   ALTER ANY CREDENTIAL 権限が必要です。  
  
-   ALTER ANY LOGIN 権限が必要です。  
  
-   CREATE ASYMMETRIC KEY 権限が必要です。  
  
-   データベースを暗号化するには、データベースに対する CONTROL 権限が必要です。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-enable-tde-using-ekm"></a>EKM を使用して TDE を有効にするには  
  
1.  EKM プロバイダーによって提供されるファイルを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] コンピューターの適切な場所にコピーします。 この例では、 **C:\EKM** フォルダーを使用します。  
  
2.  EKM プロバイダーの要件に従ってコンピューターに証明書をインストールします。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、EKM プロバイダーは用意されていません。 EKM プロバイダーごとに、インストール、構成、およびユーザー承認の手順が異なります。  この手順を完了するには、EKM プロバイダーのドキュメントを参照してください。  
  
3.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。  
  
4.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
5.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- Enable advanced options.  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Create a cryptographic provider, which we have chosen to call "EKM_Prov," based on an EKM provider  
  
    CREATE CRYPTOGRAPHIC PROVIDER EKM_Prov   
    FROM FILE = 'C:\EKM_Files\KeyProvFile.dll' ;  
    GO  
  
    -- Create a credential that will be used by system administrators.  
    CREATE CREDENTIAL sa_ekm_tde_cred   
    WITH IDENTITY = 'Identity1',   
    SECRET = 'q*gtev$0u#D1v'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
    GO  
  
    -- Add the credential to a high privileged user such as your   
    -- own domain login in the format [DOMAIN\login].  
    ALTER LOGIN Contoso\Mary  
    ADD CREDENTIAL sa_ekm_tde_cred ;  
    GO  
    -- create an asymmetric key stored inside the EKM provider  
    USE master ;  
    GO  
    CREATE ASYMMETRIC KEY ekm_login_key   
    FROM PROVIDER [EKM_Prov]  
    WITH ALGORITHM = RSA_512,  
    PROVIDER_KEY_NAME = 'SQL_Server_Key' ;  
    GO  
  
    -- Create a credential that will be used by the Database Engine.  
    CREATE CREDENTIAL ekm_tde_cred   
    WITH IDENTITY = 'Identity2'   
    , SECRET = 'jeksi84&sLksi01@s'   
    FOR CRYPTOGRAPHIC PROVIDER EKM_Prov ;  
  
    -- Add a login used by TDE, and add the new credential to the login.  
    CREATE LOGIN EKM_Login   
    FROM ASYMMETRIC KEY ekm_login_key ;  
    GO  
    ALTER LOGIN EKM_Login   
    ADD CREDENTIAL ekm_tde_cred ;  
    GO  
  
    -- Create the database encryption key that will be used for TDE.  
    USE AdventureWorks2012 ;  
    GO  
    CREATE DATABASE ENCRYPTION KEY  
    WITH ALGORITHM  = AES_128  
    ENCRYPTION BY SERVER ASYMMETRIC KEY ekm_login_key ;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE AdventureWorks2012   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
 詳細については、「  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
-   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
-   [Azure Key Vault を使用する拡張キー管理 &#40;SQL Server&#41;](extensible-key-management-using-azure-key-vault-sql-server.md)  
  
-   [Azure SQL Database での Transparent Data Encryption](../../../database-engine/transparent-data-encryption-with-azure-sql-database.md)  
  
  
