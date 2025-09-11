This is a breakdown hot to make fake shadow for animated objects since Meta Horizon engine doesn't support
dynamic shadows for non-static object.

<img src="Content/intro.gif" alt="Demo" width="600">

Here is example the final result which is available as remixable world 


First of all we need to setup our Asset Template that going to be spawned in the world.
The asset hierarchy is non-trivial to set-up because we need the object to be physical and unfortunatly 
current vesrion of the engine doesn't handle well transformations of child objects in the hierarchy. That
why we need special structure in order to do that.

Lets start to do that. We are going to make it on simple cube.

First of all spawn place a cube. And call it CubeMesh

<img src="Content/image1.png" alt="Step 1" width="500">

For the outline mesh we use custom created mesh in any DCC app like Maya or blender with inverted
normals. We import this mesh in MHW with unlit material, you can read more here how to do that
https://developers.meta.com/horizon-worlds/learn/documentation/custom-model-import/creating-custom-models-for-horizon-worlds/materials-guidance-and-reference-for-custom-models



for the shadow we use simple texture with alpha, important note that in order to apply this texture
you should have plane model with Unlit Blend Material set up. You can get this texture in Content folder 
of this tutorial

<img src="Content/ShadowPlane_BA.png" alt="Step 1" width="256">

place this plane together with created cube, and outline mesh

<img src="Content/image2.png" alt="Step 1" width="1000">

your initial setup will look like this:'
CubeMesh, Outline, ShadowPlane stacked one after another.

the next step is to start creating right hierarchy. Lets create parent object for CubeMesh and Outline and call it
CubeView

<img src="Content/image3.png" alt="Step 1" width="500">

Now lets create another parent object of View and ShadowPlane.  So eventually hierarchy of object
will look like this

<img src="Content/image5.png" alt="Step 1" width="500">

Now the most important step is to setup correct behaviour of each object in the hierarchy

<img src="Content/image6.png" alt="Step 1" width="1000">

- Root object Cube0 left unchanged
- CubeView that hold CubeMesh and Outline motion parameter should be set to Interactive
- CubeMesh and Outline Motion type should be Animated
- ShadowPlane Motion type should also be Animated but Collidable option should be turned off

Here is how my 3 cubes eventualy looks like

<img src="Content/image7.png" alt="Step 1" width="1000">


OK lets move forward to scripts that controls shadows.
All system basically consists of 2 scripts ISelectable and FakeShadows
ISelectable is attached to each cube and pritty straight forward. Its just hold 
all data we need for outline and fake shadows to work

Each cube has script called ISelectable attached, since my objects can be selected by user
and moved

```ts
import { FakeShadows } from 'FakeShadows';
import * as hz from 'horizon/core';
import { PropTypes, Entity, Quaternion} from 'horizon/core';
import { Utils } from 'Utils';

export class ISelectable extends hz.Component<typeof ISelectable> {
static propsDefinition = {
outline: { type: PropTypes.Entity },
shadow: { type: PropTypes.Entity },
id: { type: PropTypes.Number }
};

    private deltaRotation: Quaternion = Quaternion.zero;

    GetId(): number {
        return this.props.id;
    }

    start() {
        if (!Utils.ChangeOwnershipToLocal(this)) return; 
        var outline = this.props.outline?.as(Entity);
        FakeShadows.Register(this);
        outline?.visible.set(false);
    }
    
    ShadowPlane(): Entity {
        if (this.props.shadow)
            return this.props.shadow;
        return this.entity;
    }

    DeltaRotation(): Quaternion {
        return this.deltaRotation;
    }

    ShowOutline() {
        var outline = this.props.outline?.as(Entity);
        outline?.visible.set(true);
    }

    HideOutline() {
        var outline = this.props.outline?.as(Entity);
        outline?.visible.set(false);
    }

}
hz.Component.register(ISelectable);
``` 

The second one is FakeShadow where the all math done

```ts
import * as hz from 'horizon/core';
import { Entity, Quaternion, World, EventSubscription } from 'horizon/core';
import { ISelectable } from 'ISelectable';
import { Utils } from 'Utils';

export class FakeShadows extends hz.Component<typeof FakeShadows> {

    private static selectables: ISelectable[] = [];

    start(): void 
    {
    }

    public static Register(selectable: ISelectable): void {
        this.selectables[this.selectables.length] = selectable;
    }

    preStart() {
        if (!Utils.ChangeOwnershipToLocal(this)) return;
        this.connectLocalBroadcastEvent(World.onUpdate, (deltaTime) => {
            FakeShadows.selectables.forEach(element => {
                this.update(element.entity, element.ShadowPlane(), element.DeltaRotation());
            });
        });
    }

    private GetYaw(q: Quaternion): Quaternion {
        var yaw = Math.atan2(
            2 * (q.y * q.w + q.x * q.z),
            1 - 2 * (q.y * q.y + q.z * q.z)
        );
        return new Quaternion(0, Math.sin(yaw / 2), 0, Math.cos(yaw / 2));
    }

    private update(parent: Entity, shadowPlane: Entity, deltaRotation: Quaternion): void {
        if (shadowPlane) {
            var position = parent.position.get();
            position.y = 0.1;
            shadowPlane.rotation.set(this.GetYaw(parent.rotation.get()).mul(this.GetYaw(deltaRotation)));
            shadowPlane.position.set(position);
        }
    }
}
hz.Component.register(FakeShadows);
```