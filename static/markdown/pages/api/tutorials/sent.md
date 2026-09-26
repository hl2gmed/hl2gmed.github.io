# Tutorials — First Scripted Entity<hr>

```lua
ENT.Type = "anim"
ENT.Base = "base_anim"


-- The name that appears in the spawnmenu.
ENT.PrintName   = "Explosive Barrel"
ENT.Information = "Shoot to explode."
ENT.Author      = "You!"

ENT.Spawnable = true

-- These are custom entity variables, feel free to change them!
ENT.ExplosionDamage = 100
ENT.ExplosionRadius = 250

-- This custom variable prevents the entity from infinitely exploding.
ENT.HasExploded = false

-- This code runs whenever the entity is created.
function ENT:Initialize()
	self:SetModel( "models/props_c17/oildrum001_explosive.mdl" )

	-- Only set up physics on the server since it tends to create weird issues if you do it on the client.
	if SERVER then
		self:PhysicsInit( SOLID_VPHYSICS )
		self:SetMoveType( MOVETYPE_VPHYSICS )
		self:SetSolid( SOLID_VPHYSICS )
	end

	local phys = self:GetPhysicsObject()

	-- This will make the entity fall instead of being stuck in the air when spawned.
	if ( IsValid( phys ) ) then
		phys:Wake()
	end

	-- This is required to allow the entity to be gibbed.
	if ( SERVER ) then
		self:PrecacheGibs()
	end
end

-- Explode when damaged!
function ENT:OnTakeDamage( damageInfo )
	if self.HasExploded then
		return -- Stop the code here if the entity already exploded.
	end
    
	local newEffectData = EffectData() -- Creates a new EffectData to use in util.Effect.
	newEffectData:SetOrigin( self:GetPos() )
	newEffectData:SetMagnitude( 100 )
	newEffectData:SetScale( 1 )

	-- Make the explosion effect!
	util.Effect( "Explosion", newEffectData )

	-- Makes the entity split apart. (The vector adds force to the gibs upwards)
	self:GibBreakServer( Vector( 0, 0, 10 ) )

	-- Setting this to true prevents the entity from exploding again.
	self.HasExploded = true
    
	self:Remove()
end

function ENT:OnRemove()
	if ( SERVER ) then
		-- Deal explosion damage.
		-- (The last two variables are custom and can be changed at the top)
		util.BlastDamage( self, self, self:GetPos(), self.ExplosionRadius, self.ExplosionDamage )
	end
end
```
