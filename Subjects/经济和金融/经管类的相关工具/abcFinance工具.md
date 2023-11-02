---
title: abcFinance工具
authors: Ethan Lin
year: 2022-12-29 
tags:
  - 日期/2022-12-29 
  - 类型/笔记 
  - 内容/多主体建模 
  - 内容/经济金融 
---


# abcFinance工具






# 一些概念

# 官方介绍



```python
"""
 abcFinance is an implementation of a double entry book keeping system

Initialize the accounting system with, the name of the residual_account::

    accounts = Ledger(residual_account_name='equity')

Create stock and flow account:

    accounts.make_stock_account(['cash', 'claims'])
    accounts.make_flow_account(['expenditure'])

In order to book give a list of credit and debit tuples. Each tuple should be
an account and a value::

    accounts.book(
        debit=[('cash', 50), ('claims', 50)],
        credit=[('equity', 100)])

get balance gives you the balance of an account:

    assert accounts['cash'].get_balance() == (AccountSide.DEBIT, 50)

Example::

"""
```


```python
    accounts.book(debit=[('expenditure', 20)], credit=[('cash', 20)])

    assert accounts.get_total_assets() == 80, accounts.get_total_assets()

    accounts.print_profit_and_loss()
    print('--')
    accounts.make_end_of_period()

    accounts.print_profit_and_loss()

    accounts.print_balance_sheet()

    assert accounts['equity'].get_balance() == (AccountSide.CREDIT, 80)

```



# 变量结构与内容

- `Ledger`类
	方法：
	
	- `make_..._accounts(...)`：生成某某账户。包括存量、流量、资产、负债、盈余等多个账户。
	- `book(...)`：记录一笔明细。
	
	  ```python
	      def book(self, debit, credit, text=""):
	          """ Book a transaction.  记录一笔明细
	  
	          Arguments:
	              debit, list of tuples ('account', amount)
	  
	              credit, list of tuples ('account', amount)
	  
	              text, for booking history
	  
	          Example::
	  
	              accounts.book(debit=[('inventory', 20)],
	                            credit=[('cash', 20)],
	                            text="Purchase of equipment")
	          """
	          sum_debit = 0
	          sum_credit = 0
	  
	          for name, value in debit:
	              account = self.accounts[name]  # 获取科目名
	              account.debit += value  # 借方累加
	              if name in self.asset_accounts:  # 记录资产负债表所在边
	                  side, _ = account.get_balance()
	                  assert side != AccountSide.CREDIT
	              elif name in self.liability_accounts:
	                  side, _ = account.get_balance()
	                  assert side != AccountSide.DEBIT
	              sum_debit += value
	  
	          for name, value in credit:
	              assert value >= 0
	              account = self.accounts[name]
	              account.credit += value  # 贷方累加
	              if name in self.asset_accounts:
	                  side, _ = account.get_balance()
	                  assert side != AccountSide.CREDIT
	              elif name in self.liability_accounts:
	                  side, _ = account.get_balance()
	                  assert side != AccountSide.DEBIT
	              sum_credit += value  # 累加贷方
	  
	          assert sum_debit == sum_credit
	  
	          self.booking_history.append((debit, credit, text))
	  ```
	
	  
	- `book_end_of_period(...)`：结转当期流量、借贷账户于期末。
	
	  ```python
	      def book_end_of_period(self):
	          """ Close flow accounts and credit/debit residual (equity) account 结转当期流量、借贷账户于期末 """
	          profit = 0
	          debit_accounts = []
	          credit_accounts = []
	          for name, account in self.flow_accounts.items():
	              side, balance = account.get_balance()
	              if balance > 0:
	                  if side == AccountSide.DEBIT:  # 如果余额出现在借方，则说明损失，因此收益减少其余额量，反之亦然
	                      profit -= balance
	                      credit_accounts.append((name, balance))  # 贷方账户追加一笔余额
	                  else:
	                      profit += balance
	                      debit_accounts.append((name, balance))
	  
	          if profit > 0:
	              credit_accounts.append((self.residual_account_name, profit))
	          else:
	              debit_accounts.append((self.residual_account_name, -profit))
	  
	          self.book(debit=debit_accounts,
	                    credit=credit_accounts, text='Period close')
	          self.profit_history.append((debit_accounts, credit_accounts))
	  
	          for account in self.flow_accounts:
	              account = Account()
	```
	- `get_balance(...)`：更新资产负债表。通过比较单个账户科目里的借方与贷方金额，确定帐户余额位置位于「借」或者「贷」与相应的金额。
	
	  ```python
	  def get_balance(self):
	          """
	          更新资产负债表。通过比较单个账户科目里的借方与贷方金额，确定帐户余额位置位于「借」或者「贷」与相应的金额
	          """
	          debitsum = self.debit
	          creditsum = self.credit
	          if debitsum > creditsum:
	              return (AccountSide.DEBIT, debitsum - creditsum)
	          elif debitsum == creditsum:
	              return(AccountSide.BALANCED, 0)
	          else:
	              return (AccountSide.CREDIT, creditsum - debitsum)
	  
	      def __setattr__(self, name, value):
	          if name == 'debit' and hasattr(self, 'debit'):
	              assert value >= self.debit
	          if name == 'credit' and hasattr(self, 'credit'):
	              assert value >= self.credit
	  
	          return super().__setattr__(name, value)
	  
	      def print_balance(self):
	          print('debit', self.debit)
	          print('credit', self.credit)
	  ```
	
	  






对于收到违约等冲击造成的资产小于负债的情况，该工具包直接简化，使用了负资本金填充缺失的资产部分，用以配平资产负债表。样例在：[Ex4\_Crises](https://www.siebenbrunner.com/moneycreation/Ex4_Crises.html)。