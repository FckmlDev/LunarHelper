## LunarHelper
An explanation of how LunarClient-API works.

The methods wrote next are just examples.

This method clears team info for a player.
    
    public void resetTeamInfo(Player player) {
      LunarClientAPI.getInstance().sendTeammates(player, new LCPacketTeammates(player.getUniqueId(), 100L, new HashMap<>()));
    }
  
This method adds players to a player TeamInfo.

    public void addTeamInfo(Player player, List<Player> playersToAdd) {  
        Map<UUID, Map<String, Double>> map = new ConcurrentHashMap<>();  
      
      playersToAdd.forEach(members -> {  
            Map<String, Double> position = new HashMap<>();  
      
     if (members.getPlayer() == null) return;  
      
      position.put("x", members.getPlayer().getLocation().getX());  
      position.put("y", members.getPlayer().getLocation().getY());  
      position.put("z", members.getPlayer().getLocation().getZ());  
      
      map.put(members.getUniqueId(), position);  
      });  
      
      LCPacketTeammates teammates = new LCPacketTeammates(player.getUniqueId(), 0L, map);  
      
      LunarClientAPI.getInstance().sendTeammates(player, teammates);  
    }

Note: This methods is one time, it needs to keep updating per second. (Do a runnable and use this methods beetween players.)


