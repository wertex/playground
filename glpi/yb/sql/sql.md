'''
select pc.name, u.name, soft.name, link.name, link.url from glpi.glpi_computers pc
  left join glpi.glpi_users u
  on pc.users_id = u.id
  left join glpi.glpi_items_softwareversions softiv
  on pc.id = softiv.items_id
  left join glpi.glpi_softwareversions softv
  on softv.id = softiv.softwareversions_id
  left join glpi.glpi_softwares soft
  on soft.id = softv.softwares_id
  left join glpi.glpi_manuallinks link
  on soft.id = link.items_id
  WHERE pc.states_id = 1
'''
Вытаскиваем имя ПК, пользователя, название ПО, url
