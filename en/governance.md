---
layout: default
title: Governance
lang: en
url: /en/governance
---

## Governance and Board

AP-IPS is governed by a board composed of representatives from participating countries and organizations.

### Search Board Members

<div style="margin-bottom: 20px;">
  <input type="text" id="searchName" placeholder="Search by Name" style="padding: 8px; margin-right: 10px; width: 200px;">
  <input type="text" id="searchNation" placeholder="Search by Nation" style="padding: 8px; margin-right: 10px; width: 200px;">
  <input type="text" id="searchOrg" placeholder="Search by Organization" style="padding: 8px; width: 200px;">
</div>



| Name | Nation | Organization |
|------|--------|--------------|
| **Hyoungho Do**$              | South Korea | IHE Korea                                                        |
| **Chung-Yueh Lien (連中岳)**$          | Taiwan      | MISAT, National Taipei University of Nursing and Health Sciences |
| **Yasunari Shiokawa (Salt)**$ | Japan       | IHE-Japan                                                        |
| JoonHyun Song             | South Korea | HL7 Korea                                                        |
| Tom Wang                  | Taiwan      | EBM Technologies                                                 |
| Masayoshi Seki            | Japan       | IHE-Japan                                                        |
| Takeshi Ozeki             | Japan       | IHE-Japan                                                        |
| Sunao Watanabe            | Japan       | MEDIS-DC                                                         |
| Takanori Yamashita        | Japan       | JAMI                                                             |
| Masahito Kawamori         | Japan       | University of Tokyo                                              |
| HeeKyoung Jung            | South Korea | Korea Total Healthcare Ecosystem Association                                                 |
| Yoshimasa Kawazoe         | Japan       | University of Tokyo                                              |
| Takeshi Imai              | Japan       | University of Tokyo                                              |
| Katsuhiko Nishino         | Japan       | Tokyo Metroporitan Hiroo Hospital                                |
| Kazunori Nozaki           | Japan       | University of Osaka                                              |
| Lorex Yang                | Taiwan      | Sitatech Information Services Co., Ltd                           |
| Ping Huang Tsai           | Taiwan      | TwHealth Nexus Inc                                               |
| BI-Shan Hsu               | Taiwan      | TwHealth Nexus Inc                                               |
| Simon Yu                  | Taiwan      | TwHealth Nexus Inc                                               |
| Chien-Yeh Hsu             | Taiwan      | National Taipei University of Nursing and Health Sciences        |
| Ryoichi Tanaka            | Japan       | Iwate Medical University                                         |
| Henrique Martins*         | Portugal    | ISCTE, IHE-Catalyst                                              |
| Syoji Uzawa*              | Japan       | IHE-Japan                                                        |
| Byoung-Kee Yi	            |South Korea | Kangwon National University/HL7 Korea |
|Sung-Hyun Lee	            |South Korea | Flyingmountain Inc |
|Soojin Lee	                |South Korea | Sangji university |
|Alvin Marcelo	            |Philippines | Medical Informatics Unit, University of the Philippines |

{:#boardTable}

* **Note: $Leadership**; ***Observer**

<style>
  table {
    border-collapse: collapse;
    width: 100%;
    cursor: pointer;
  }

  th, td {
    border: 1px solid black;
    padding: 8px;
    text-align: left;
  }

  th {
    background-color: #f2f2f2;
    cursor: pointer;
    user-select: none;
  }

  th:hover {
    background-color: #e0e0e0;
  }

  th::after {
    content: ' ⇅';
    font-size: 0.8em;
    opacity: 0.5;
  }
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const searchName = document.getElementById('searchName');
  const searchNation = document.getElementById('searchNation');
  const searchOrg = document.getElementById('searchOrg');
  const table = document.getElementById('boardTable');
  
  if (!table) return;
  
  const rows = table.getElementsByTagName('tr');
  let sortConfig = { column: null, direction: 'asc' };
  
  function filterTable() {
    const nameFilter = searchName.value.toLowerCase();
    const nationFilter = searchNation.value.toLowerCase();
    const orgFilter = searchOrg.value.toLowerCase();
    
    for (let i = 1; i < rows.length; i++) {
      const cells = rows[i].getElementsByTagName('td');
      if (cells.length >= 3) {
        const name = cells[0].textContent.toLowerCase();
        const nation = cells[1].textContent.toLowerCase();
        const org = cells[2].textContent.toLowerCase();
        
        const matchName = name.includes(nameFilter);
        const matchNation = nation.includes(nationFilter);
        const matchOrg = org.includes(orgFilter);
        
        if (matchName && matchNation && matchOrg) {
          rows[i].style.display = '';
        } else {
          rows[i].style.display = 'none';
        }
      }
    }
  }
  
  function sortTable(columnIndex) {
    const rowsArray = Array.from(rows).slice(1);
    
    if (sortConfig.column === columnIndex) {
      sortConfig.direction = sortConfig.direction === 'asc' ? 'desc' : 'asc';
    } else {
      sortConfig.column = columnIndex;
      sortConfig.direction = 'asc';
    }
    
    rowsArray.sort((rowA, rowB) => {
      const cellsA = rowA.getElementsByTagName('td');
      const cellsB = rowB.getElementsByTagName('td');
      
      if (cellsA.length <= columnIndex || cellsB.length <= columnIndex) {
        return 0;
      }
      
      let valueA = cellsA[columnIndex].textContent.trim();
      let valueB = cellsB[columnIndex].textContent.trim();
      
      // Remove bold markers and special characters for comparison
      valueA = valueA.replace(/\*\*/g, '').toLowerCase();
      valueB = valueB.replace(/\*\*/g, '').toLowerCase();
      
      if (sortConfig.direction === 'asc') {
        return valueA.localeCompare(valueB, 'zh-TW');
      } else {
        return valueB.localeCompare(valueA, 'zh-TW');
      }
    });
    
    const tbody = table.querySelector('tbody') || table;
    rowsArray.forEach(row => {
      tbody.appendChild(row);
    });
  }
  
  // Add click event to headers
  const headerRow = rows[0];
  const headers = headerRow.getElementsByTagName('th');
  
  for (let i = 0; i < headers.length; i++) {
    headers[i].style.cursor = 'pointer';
    headers[i].addEventListener('click', function() {
      sortTable(i);
    });
  }
  
  searchName.addEventListener('keyup', filterTable);
  searchNation.addEventListener('keyup', filterTable);
  searchOrg.addEventListener('keyup', filterTable);
});
</script>

## Member Countries
- Australia
- Japan
- Malaysia
- Singapore
- South Korea
- Taiwan