<template>
    <ion-page>
        <ion-content>
            <!-- Content -->
            <div class="content">
                <ion-label>Content</ion-label>
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Eligendi labore quis, illo, possimus dolorem et doloremque nostrum quae repellat minus tempora ea dolores? Eveniet nostrum provident, numquam quia molestiae sequi.</p>
            </div>

            <!-- Services slider cards -->
            <div class="services">
                <ion-label>Services</ion-label>
                <ion-slides pager="true" :options="slideOpts">
                    <!-- Here the app crahses -->
                    <ion-slide v-for="(service, index) in services" :key="index">
                        <ion-card>
                           {{ service.name }}
                        </ion-card>
                    </ion-slide>
                    <!-- Here the app crahses -->
                </ion-slides>
            </div>
        </ion-content>
    </ion-page>
</template>

<script lang="ts">
import { IonContent, IonPage, IonSlides, IonSlide, IonLabel, IonCard } from '@ionic/vue';
import { defineComponent, onMounted, ref } from 'vue';

// Service interface
interface Service {
    name: string;
}

export default defineComponent({
    name: 'Home',
    components: {
        IonContent,
        IonPage,
        IonSlides,
        IonSlide,
        IonCard,
        IonLabel
    },
    setup() {
        // Declare services data array
        const services = ref<Service[]>([]);

        // Slider Options
        const slideOpts = {
            speed: 400,
            initialSlide: 0,
            slidesPerView: 2,
            spaceBetween: 190,
            centeredSlides: true,
        };

        onMounted(() => {
            // Simulate HTTP Request to fill the array
            setTimeout(() => {
                const data = [
                    {
                        name: 'Slide 1'
                    },
                    {
                        name: 'Slide 2'
                    },
                    {
                        name: 'Slide 3'
                    },
                ];

                services.value.push(...data)
            }, 2000);
        })

        return {
            slideOpts,
            services
        }
    }
});
</script>

<style scoped>
.content, .services {
    text-align: center;
}

ion-card {
    min-width: 280px;
    min-height: 350px;
}
</style>