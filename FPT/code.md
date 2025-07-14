

```javascript

show: async (req) => {
        const { id } = req.params
        const profile = req?.user
        const house =

            await ProfileHouseService.findOneWithTotalRoomAndDeviceById(
                id,
                profile.id
            )

        if (!house) {

            return {

                status: 404,

                message: getMessage(req?.query?.lang, 'houses.house_not_found'),

                time: getTimeNow(),

            }

        }

        return {

            status: 200,

            message: getMessage(req?.query?.lang, 'default.success'),

            data: house,

            time: getTimeNow(),

        }

        // ============= END ===============

    }

```

