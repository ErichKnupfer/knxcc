# knxcc

import org.bukkit.Bukkit;
import org.bukkit.Location;
import org.bukkit.Material;
import org.bukkit.World;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerInteractEvent;
import org.bukkit.event.player.PlayerJoinEvent;
import org.bukkit.util.Vector;


public class Listeners implements Listener {

    public static Location toLocation(World world, double x, double y, double z) {
        return new Location(world, x, y, z);
    }

    @EventHandler
    public void onJoin(PlayerJoinEvent e) {
        Player p = e.getPlayer();
        p.hasPermission("knxcc.join");
        Bukkit.getServer().broadcastMessage("§b§l!§r §a" + p.getName() + "§e, joined!");
    }

    @EventHandler
    public void onPlayerInteract(PlayerInteractEvent event) {

        Location eyeLocation = event.getPlayer().getEyeLocation();
        Vector direction = event.getPlayer().getEyeLocation().getDirection();
        direction.multiply(50);
        Location targetLocation = eyeLocation.add(direction);

        if (event.getPlayer().getItemInHand().getType() == Material.GOLDEN_AXE) ;
        event.getPlayer().getWorld().strikeLightning(event.getClickedPosition().toLocation(targetLocation.getWorld()));

    }
}
