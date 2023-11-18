
#### Excel 다루기
> [Openpyxl 라이브러리](https://openpyxl.readthedocs.io/en/stable/)
```python
# openpyxl 간단 사용법
from openpyxl import Workbook
wb = Workbook() # Workbook 객체 생성
ws = wb.active # 활성화된 Worksheet 객체 가져오기
ws.append(['A', 'B']) # 로우를 리스트로 한번에 삽입
ws['A2'] = 1 # 특정 셀에 값 삽입
ws.cell(row=1, column=2).value # 값확인
ws.cell(row=1, column=2).value = 2 # 값삽입
ws.cell(row=1, column=2, value=3) # 값삽입
ws.max_row # 최대 row
ws.max_column # 최대 column 
```