# Spring MVC 咖啡訂單管理系統 ⚡

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.5-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![Spring MVC](https://img.shields.io/badge/Spring%20MVC-6.0-blue.svg)](https://spring.io/projects/spring-framework)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 專案介紹

這是一個基於Spring Boot和Spring MVC的咖啡訂單管理系統，提供RESTful API來處理咖啡訂單的創建和查詢。系統採用現代化的微服務架構，具備高可擴展性和易維護性。

### 核心功能
- **咖啡管理**：提供咖啡品項的查詢功能
- **訂單處理**：支援創建新訂單，包含客戶資訊和咖啡品項
- **狀態管理**：訂單狀態追蹤（初始化、已付款、沖煮中、已完成、已取貨、已取消）
- **快取機制**：使用Spring Cache提升查詢效能

> 💡 **為什麼選擇此專案？**
> - 採用Spring Boot 3.x最新技術棧，支援Java 21
> - 使用Jakarta Persistence API，符合最新JPA標準
> - 整合H2記憶體資料庫，便於開發和測試
> - 支援Lombok，減少樣板程式碼

### 🎯 專案特色

- **RESTful API設計**：遵循REST架構原則，提供清晰的API端點
- **資料庫整合**：使用JPA/Hibernate進行物件關聯對應
- **快取優化**：整合Spring Cache提升系統效能
- **貨幣處理**：支援Joda Money處理精確的貨幣計算
- **交易管理**：使用Spring Transaction確保資料一致性

## 技術棧

### 核心框架
- **Spring Boot 3.4.5** - 快速開發框架，提供自動配置和內嵌伺服器
- **Spring MVC 6.0** - Web應用程式框架，處理HTTP請求和回應
- **Spring Data JPA** - 資料存取層框架，簡化資料庫操作
- **Spring Cache** - 快取抽象層，提升應用程式效能

### 開發工具與輔助
- **Lombok** - 減少樣板程式碼，自動生成getter/setter等方法
- **H2 Database** - 輕量級記憶體資料庫，適合開發和測試
- **Joda Money** - 精確的貨幣處理庫
- **Maven** - 專案建置和依賴管理工具

## 專案結構

```
simple-controller-demo/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── tw/fengqing/spring/springbucks/waiter/
│   │   │       ├── WaiterServiceApplication.java          # 主應用程式入口
│   │   │       ├── controller/                            # 控制器層
│   │   │       │   ├── CoffeeController.java             # 咖啡相關API
│   │   │       │   ├── CoffeeOrderController.java        # 訂單相關API
│   │   │       │   └── request/
│   │   │       │       └── NewOrderRequest.java          # 訂單請求DTO
│   │   │       ├── model/                                # 實體模型層
│   │   │       │   ├── BaseEntity.java                   # 基礎實體類別
│   │   │       │   ├── Coffee.java                       # 咖啡實體
│   │   │       │   ├── CoffeeOrder.java                  # 訂單實體
│   │   │       │   ├── OrderState.java                   # 訂單狀態列舉
│   │   │       │   └── MoneyConverter.java               # 貨幣轉換器
│   │   │       ├── repository/                           # 資料存取層
│   │   │       │   ├── CoffeeRepository.java             # 咖啡資料存取
│   │   │       │   └── CoffeeOrderRepository.java        # 訂單資料存取
│   │   │       └── service/                              # 業務邏輯層
│   │   │           ├── CoffeeService.java                # 咖啡業務邏輯
│   │   │           └── CoffeeOrderService.java           # 訂單業務邏輯
│   │   └── resources/
│   │       ├── application.properties                     # 應用程式設定檔
│   │       ├── data.sql                                  # 初始資料
│   │       └── schema.sql                                # 資料庫結構
│   └── test/
│       └── java/
│           └── tw/fengqing/spring/springbucks/waiter/
│               └── WaiterServiceApplicationTests.java     # 整合測試
├── pom.xml                                               # Maven專案配置
└── README.md                                             # 專案說明文件
```

## 快速開始

### 前置需求
- **Java 21** - 確保已安裝JDK 21或更新版本
- **Maven 3.6+** - 專案建置工具
- **IDE** - 建議使用IntelliJ IDEA或VS Code

### 安裝與執行

1. **克隆此倉庫：**
```bash
git clone https://github.com/SpringMicroservicesCourse/spring-controller-demo.git
```

2. **進入專案目錄：**
```bash
cd simple-controller-demo
```

3. **編譯專案：**
```bash
mvn clean compile
```

4. **執行應用程式：**
```bash
mvn spring-boot:run
```

5. **驗證應用程式：**
```bash
curl http://localhost:8080/coffee/
```

## API 端點說明

### 咖啡相關API

| 方法 | 端點 | 說明 | 請求範例 |
|------|------|------|----------|
| GET | `/coffee/` | 獲取所有咖啡品項 | `curl http://localhost:8080/coffee/` |

### 訂單相關API

| 方法 | 端點 | 說明 | 請求範例 |
|------|------|------|----------|
| POST | `/order/` | 創建新訂單 | ```bash
curl -X POST http://localhost:8080/order/ \
  -H "Content-Type: application/json" \
  -d '{
    "customer": "張三",
    "items": ["espresso", "latte"]
  }'
``` |

## 進階說明

### 環境變數
```properties
# 資料庫設定
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver

# JPA設定
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=create-drop

# 快取設定
spring.cache.type=caffeine
```

### 設定檔說明
```properties
# application.properties 主要設定
# 資料庫連線設定
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.username=sa
spring.datasource.password=

# JPA/Hibernate設定
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# 快取設定
spring.cache.type=caffeine
spring.cache.cache-names=CoffeeCache
```

## 重要程式碼說明

### 實體模型設計
```java
/**
 * 咖啡實體類別
 * 使用JPA註解進行物件關聯對應
 * 整合Lombok減少樣板程式碼
 */
@Entity
@Table(name = "T_COFFEE")
@Builder
@Data
@EqualsAndHashCode(callSuper = true)
@ToString(callSuper = true)
@NoArgsConstructor
@AllArgsConstructor
public class Coffee extends BaseEntity implements Serializable {
    private String name;
    
    /**
     * 使用自定義轉換器處理貨幣類型
     * 確保貨幣計算的精確性
     */
    @Convert(converter = MoneyConverter.class)
    private Money price;
}
```

### 控制器設計
```java
/**
 * 訂單控制器
 * 處理訂單相關的HTTP請求
 * 使用@RestController提供RESTful API
 */
@RestController
@RequestMapping("/order")
@Slf4j
public class CoffeeOrderController {
    
    /**
     * 創建新訂單
     * @param newOrder 訂單請求物件
     * @return 創建的訂單實體
     */
    @PostMapping("/")
    @ResponseStatus(HttpStatus.CREATED)
    public CoffeeOrder create(@RequestBody NewOrderRequest newOrder) {
        log.info("Receive new Order {}", newOrder);
        Coffee[] coffeeList = coffeeService.getCoffeeByName(newOrder.getItems())
                .toArray(new Coffee[] {});
        return orderService.createOrder(newOrder.getCustomer(), coffeeList);
    }
}
```

## 參考資源

- [Spring Boot 官方文件](https://spring.io/projects/spring-boot)
- [Spring MVC 參考指南](https://docs.spring.io/spring-framework/reference/web/webmvc.html)
- [Spring Data JPA 文件](https://spring.io/projects/spring-data-jpa)
- [H2 Database 文件](https://www.h2database.com/html/main.html)
- [Joda Money 文件](https://www.joda.org/joda-money/)

## 注意事項與最佳實踐

### ⚠️ 重要提醒

| 項目 | 說明 | 建議做法 |
|------|------|----------|
| 資料庫連線 | 生產環境資料庫配置 | 使用外部資料庫（如PostgreSQL、MySQL） |
| 安全性 | API安全防護 | 整合Spring Security |
| 效能 | 快取策略 | 根據業務需求調整快取配置 |
| 日誌記錄 | 系統監控 | 整合Logback或Log4j2 |

### 🔒 最佳實踐指南

- **程式碼註解**：在重要的程式碼區塊添加清楚註解，方便團隊成員理解與維護
- **異常處理**：使用統一的異常處理機制，提供友善的錯誤訊息
- **API文件**：整合Swagger/OpenAPI自動生成API文件
- **單元測試**：為核心業務邏輯撰寫完整的單元測試
- **程式碼品質**：使用SonarQube等工具確保程式碼品質

## 授權說明

本專案採用 MIT 授權條款，詳見 LICENSE 檔案。

## 關於我們

我們主要專注在敏捷專案管理、物聯網（IoT）應用開發和領域驅動設計（DDD）。喜歡把先進技術和實務經驗結合，打造好用又靈活的軟體解決方案。

## 聯繫我們

- **FB 粉絲頁**：[風清雲談 | Facebook](https://www.facebook.com/profile.php?id=61576838896062)
- **LinkedIn**：[linkedin.com/in/chu-kuo-lung](https://www.linkedin.com/in/chu-kuo-lung)
- **YouTube 頻道**：[雲談風清 - YouTube](https://www.youtube.com/channel/UCXDqLTdCMiCJ1j8xGRfwEig)
- **風清雲談 部落格**：[風清雲談](https://blog.fengqing.tw/)
- **電子郵件**：[fengqing.tw@gmail.com](mailto:fengqing.tw@gmail.com)

---

**📅 最後更新：2025-07-08**  
**👨‍💻 維護者：風清雲談團隊** 