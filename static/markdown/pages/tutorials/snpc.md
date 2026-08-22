# Introduction
**Scripted NPCs** (or **SNPCs** for short) are custom npcs coded entirely in Lua. This tutorial will go over the steps for a simple AI that will search for enemies (you) and chase them until they die or are too far away. It will also do some random other stuff when there are not any enemies.


# Lets get started
First create the npc_ folder for your npc. The one I made for this tutorial is in "custom/Npc_tut/lua/npcs" and is named "npc_simple_ai" and has "init.lua" file inside. Now open that file so you can start adding the code.

# The code
## The basic stuff we need for npcs
Start off with defining the type npc to use and making it spawnable. Pretty much the same as any other npc so far. Here we set the model and define some variables we will use later.
```lua
NPC.Type 			= "CAI_BaseNPC"
NPC.Spawnable		= true

function NPC:Initialize()

	self:SetModel( "models/antlion.mdl" )
	
	self.LoseTargetDist	= 2000	-- How far the enemy has to be before we lose them
	self.SearchRadius 	= 1000	-- How far to search for enemies
```
## Enemy related stuff
This adds some useful functions for enemy related stuff. An NPC isn't complete if it can't target stuff, right? These include a function to check if there is still an enemy or if it got away and a function to search for enemies. I've added all sorts of comments so you know exactly what they do.
```lua
   -- NPC:Get/SetEnemy()
   -- Simple functions used in keeping our enemy saved
   ----------------------------------------------------
   function self.SetEnemy(self, ent)
      self.Enemy = ent
   end

   function self.GetEnemy(self)
      return self.Enemy
   end
   ----------------------------------------------------
   -- NPC:HaveEnemy()
   -- Returns true if we have an enemy
   ----------------------------------------------------
   function self.HaveEnemy(self)
      -- If our current enemy is valid
      if ( self:GetEnemy() ) then
         -- If the enemy is too far
         if ( self:GetPos():DistTo(self:GetEnemy():GetPos()) > self.LoseTargetDist ) then
            -- If the enemy is lost then call FindEnemy() to look for a new one
            -- FindEnemy() will return true if an enemy is found, making this function return true
            return self:FindEnemy()
         -- If the enemy is dead( we have to check if its a player before we use Alive() )
         elseif ( self:GetEnemy():IsPlayer() and !self:GetEnemy():IsAlive() ) then
            return self:FindEnemy()		-- Return false if the search finds nothing
         end	
         -- The enemy is neither too far nor too dead so we can return true
         return true
      else
         -- The enemy isn't valid so lets look for a new one
         return self:FindEnemy()
      end
   end

   ----------------------------------------------------
   -- NPC:FindEnemy()
   -- Returns true and sets our enemy if we find one
   ----------------------------------------------------
   function self.FindEnemy(self)
      -- Search around us for entities
      local _, _ents = util.EntitiesInSphere( 64, self:GetPos(), self.SearchRadius, 0 )
      -- Here we loop through every entity the above search finds and see if it's the one we want
      for k,v in pairs( _ents ) do
         if v:IsPlayer() then
            -- We found one so lets set it as our enemy and return true
            self:SetEnemy(v)
            return true
         end
   	end	
      -- We found nothing so we will set our enemy as nil (nothing) and return false
      self:SetEnemy(nil)
      return false
   end

end
```
## The "brain" of our bot
As scary as this code may look to some, it is actually pretty simple:

Check if we have an enemy, if not it will look for one using the above HaveEnemy() function.
* If there is an enemy then play run at the player.
* If there are not any enemies, then walk to the last spot.
* Not that bad right? Have a look at the code, I've flooded it with comments so you should know what everything does
```lua
----------------------------------------------------
-- NPC:Think()
-- This is where the mind of our AI is
----------------------------------------------------
function NPC:Think()
	-- This function is called each tick, it acts as a giant loop that will run as long as the NPC exists
	-- Lets use the above mentioned functions to see if we have/can find a enemy
	if self:HaveEnemy() then
      -- Now that we have a enemy, the code in this block will run
      local dir = (self:GetPos()) - (self:GetEnemy():GetPos())
      local ang = QAngle()
      mathlib.VectorAngles( dir, ang )
      self:SetAbsAngles( QAngle( 0, ang.y - 180, 0 ) )	  -- Face our enemy
      self:SetSequence( self:LookupSequence( "ACT_RUN" ) ) -- Set the animation
      self:WalkMove( self:GetForward() * 32 )              -- Run forward
      -- Now once the above function is finished doing what it needs to do, the code will loop back to the start
      -- unless you put stuff after the if statement. Then that will be run before it loops
   else
      -- Since we can't find an enemy, lets wander
      self:SetSequence( self:LookupSequence( "ACT_WALK" ) ) -- Walk animation
		self:WalkMove( self:GetForward() * 19 )               -- Walk forward

	end

   self:SetNextThink( gpGlobals.curtime() + 1 ) -- Set the tickrate for Think()

end
```

# Challenges
You now have a basic npc running around the map and that's pretty much it. Here are some things you can try on your own to spice it up:

* Search for more then just players
* Play sounds when its wandering around.
* Only search for enemies that are in front of it, not all around.
* Make it hide if the enemy is holding a shotgun.
* Stop chasing the enemy when it's really close and do a melee attack.

# The full code
```lua
NPC.Type 			= "CAI_BaseNPC"
NPC.Spawnable		= true

function NPC:Initialize()

   self:SetModel( "models/antlion.mdl" )
	
   self.LoseTargetDist	= 2000	-- How far the enemy has to be before we lose them
   self.SearchRadius 	= 1000	-- How far to search for enemies

   -- NPC:Get/SetEnemy()
   -- Simple functions used in keeping our enemy saved
   ----------------------------------------------------
   function self.SetEnemy(self, ent)
      self.Enemy = ent
   end

   function self.GetEnemy(self)
      return self.Enemy
   end
   ----------------------------------------------------
   -- NPC:HaveEnemy()
   -- Returns true if we have an enemy
   ----------------------------------------------------
   function self.HaveEnemy(self)
      -- If our current enemy is valid
      if ( self:GetEnemy() ) then
         -- If the enemy is too far
         if ( self:GetPos():DistTo(self:GetEnemy():GetPos()) > self.LoseTargetDist ) then
            -- If the enemy is lost then call FindEnemy() to look for a new one
            -- FindEnemy() will return true if an enemy is found, making this function return true
            return self:FindEnemy()
         -- If the enemy is dead( we have to check if its a player before we use Alive() )
         elseif ( self:GetEnemy():IsPlayer() and !self:GetEnemy():IsAlive() ) then
            return self:FindEnemy()		-- Return false if the search finds nothing
         end	
         -- The enemy is neither too far nor too dead so we can return true
         return true
      else
         -- The enemy isn't valid so lets look for a new one
         return self:FindEnemy()
      end
   end

   ----------------------------------------------------
   -- NPC:FindEnemy()
   -- Returns true and sets our enemy if we find one
   ----------------------------------------------------
   function self.FindEnemy(self)
      -- Search around us for entities
      local _, _ents = util.EntitiesInSphere( 64, self:GetPos(), self.SearchRadius, 0 )
      -- Here we loop through every entity the above search finds and see if it's the one we want
      for k,v in pairs( _ents ) do
         if v:IsPlayer() then
            -- We found one so lets set it as our enemy and return true
            self:SetEnemy(v)
            return true
         end
   	end	
      -- We found nothing so we will set our enemy as nil (nothing) and return false
      self:SetEnemy(nil)
      return false
   end

end

----------------------------------------------------
-- NPC:Think()
-- This is where the mind of our AI is
----------------------------------------------------
function NPC:Think()
	-- This function is called each tick, it acts as a giant loop that will run as long as the NPC exists
	-- Lets use the above mentioned functions to see if we have/can find a enemy
	if self:HaveEnemy() then
      -- Now that we have a enemy, the code in this block will run
      local dir = (self:GetPos()) - (self:GetEnemy():GetPos())
      local ang = QAngle()
      mathlib.VectorAngles( dir, ang )
      self:SetAbsAngles( QAngle( 0, ang.y - 180, 0 ) )	  -- Face our enemy
      self:SetSequence( self:LookupSequence( "ACT_RUN" ) ) -- Set the animation
      self:WalkMove( self:GetForward() * 32 )              -- Run forward
      -- Now once the above function is finished doing what it needs to do, the code will loop back to the start
      -- unless you put stuff after the if statement. Then that will be run before it loops
   else
      -- Since we can't find an enemy, lets wander
      self:SetSequence( self:LookupSequence( "ACT_WALK" ) ) -- Walk animation
		self:WalkMove( self:GetForward() * 19 )               -- Walk forward

	end

   self:SetNextThink( gpGlobals.curtime() + 1 ) -- Set the tickrate for Think()

end
```
